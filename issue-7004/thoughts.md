# Thoughts

June 5th 2020

So, today I finally picked up this issue again to properly
complete it. It's been hanging around for months. It was
reviewed very late and I took lot of time to respond to
the reviews. Anyways. Now. I have fixed the tests related
to the issue and written all the code and tests.

But when running all the tests, many of them are failing.
Most of them seem to give the same error "release not found".
It's supposed to be using this in-memory release storage / driver,
but it's not working for some reason. I have to see what's going on.
I still haven't tried running the tests in master, probably I should
do that first. I started simply debugging just one test to see what's
going wrong. Still on it!

Actually even the `master` branch tests didn't run for me! 😅

I have pushed the code to see what the CI thinks. I can see that
the `master` branch circle CI tests are passing. Hmm..


