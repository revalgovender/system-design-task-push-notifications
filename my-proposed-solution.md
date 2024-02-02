# System Design Task - Push Notifications

## Considerations

- My proposed solution used the company's engineering values to guide my decision-making:
    1. Customer value and company value
    2. Speed (time-to-market, not solution performance)
    3. Simplicity

## MVP

- Send push notifications to users
    - Target specific users
    - Target multiple users

## My proposed solution

- Implement this feature in the monolith using Firebase to send push notifications

## Specific users

- Mobile devices will have device tokens
- We will store these tokens in our database
- The monolith will automatically trigger push notifications, via the Celery to queue, to Firebase
- Firebase will send the push notifications to the devices

## Multiple users

- Firebase will have a topic for each type of push notification
- The monolith will manually trigger these notifications, via the Celery queue, to Firebase
- Firebase will send the push notifications to everyone subscribed to the topic

## Why is the proposed solution a good fit?

- Keeping things in the Monolith means we can move fast
- No additional infrastructure is required which reduces complexity of the task
- Using a managed service like Firebase means we don't have to worry about scaling and reduces effort
- Overall, the solution is efficient. It will get us to market quicker. The customers and company will see value sooner.

## Why Firebase?

- No need to reinvent the wheel
- Firebase is a managed service
- It is free to send push notifications
- Provides analytics and monitoring
- Saves us development time and money
- Sends to both iOS and Android devices

## Trade-offs

- Tightly coupled to Firebase:
    - Implementing a complex pattern to allow for swapping out of vendor adds some complexity
    - We are prepping for a scenario that may never happen
    - We can refactor later but the frontend will need to be updated and the management of tokens will need to be
      migrated anyway
    - So implementing a pattern like this now will not add a lot of value
- Solution implemented within the Monolith
    - Having a separate service or event sourcing approach, would be better for management and deployment, independent
      of the Monolith
    - But this would add complexity
    - Having a separate service usually means it will scale better - however Firebase is doing all the heavy lifting for
      us
- No backend for non-technical admins
    - It would be useful for admins to be able to send push notifications manually by pressing a button and have the
      ability to
      target specific users
    - This can be a future feature

## Concerns - scale of push notifications for specific events

- We might end up sending millions of push notifications for specific events
- Events such as when earnings increase, might happen to a lot of users on the same day
- We don't want to overwhelm the Monolith
- We could start by sending push notifications to a small group (certain companies) of users and then scale up
- If the Monolith begins to be overwhelmed, we can move this functionality to a separate service
- Something like a Lambda function might be ideal for something like this
- We would also have to consider increasing queue workers for Celery