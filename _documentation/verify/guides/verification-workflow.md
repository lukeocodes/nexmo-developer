---
title: Verification workflow
description: The steps you need to take to verify a user's phone number.
navigation_weight: 1
---

# Verification Workflow

This is the workflow for verifying a user's phone number using the Verify API:

1. [Send a verification code](#send-a-verification-code) to the user and receive the `request_id` from Nexmo
2. The user receives a verification code on their phone via SMS or TTS (text-to-speech)
3. The user enters the verification code in your application
4. [Check the verification code](#check-the-verification-code) by making a request to the Verify API using the `request_id` and the code the user provides

You can optionally [cancel a verification request](#cancel-a-verification-request) or [trigger the next verification attempt](#trigger-the-next-verification-attempt) to advance from SMS message verification to TTS verification.

> For a full explanation of the verification steps and the timings associated with them, see [verification stages](verification-stages).

## Send a verification code

When you have collected a user's phone number, start the verification process by sending a [verify request](/verify/building-blocks/send-verify-request) to the Verify API.

The Verify API returns a `request_id`. You use this to identify a specific verification request in subsequent calls to the API.

## Check the verification code

Your application should provide a form or some other facility for the user to enter the verification code that they received. Make a [check request](/verify/building-blocks/check-verify-request) to the Verify API with the `request_id` and the code the user submitted. The API will tell you if the code the user supplied is the same as the one that was sent.

## Cancel a verification request

If the user decides to cancel the verification process, you should send a [cancel request](/verify/building-blocks/cancel-verify-request) to the Verify API. This will terminate the verification process even if the user supplied the correct code.

## Trigger the next verification attempt

The Verify API starts the verification process by sending an SMS to the user. If the user does not confirm the code that they received within a [certain time period](verification-stages), the Verify API makes a second verification attempt using TTS.

You can advance to the next verification attempt programmatically by making a [control request](/verify/building-blocks/trigger-next-verification-process). You would normally do this if your user indicates that they prefer to verify via a phone call instead of by SMS.

