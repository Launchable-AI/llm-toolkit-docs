# Events

## Message Generation Complete (Data Container)

This event will fire when a Chat Completion (streaming) event completes.  Use this to store message history in the database, update a user's token usage, or trigger another workflow.

## Encountered Error (Data Container)

This event will fire when the Data Container encounters an issue with Chat Completion or another action.  You can inspect the Data Container's Error Message to see what went wrong.

## Function Call Generated (Data Container)

This event will fire when the Data Container generates a function call, as a result of a Chat Completion action.  In other words, if the response that you receive back from OpenAI is a function call, this event will fire.  You can use this trigger to run "Execute Function Call", which can then call out to external APIs and services.

## Run Completed (Assistants Container)

This event fires when a run is completed.  Use this to execute further steps in your workflow, like saving data to the database, trigger a follow-up run, etc.

## Thread Created (Assistants Container)

This event fires when a Thread is first created.  This can be useful for storing the Thread ID in the database, so that you can retrieve it later.

## Transcription Complete (Audio Container)

This event fires when an audio file/recording is finished processing.
