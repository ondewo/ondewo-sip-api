# Release History

*****************

## Release ONDEWO SIP API 5.5.0

### New Features

* [[OND233-367]](https://ondewo.atlassian.net/browse/OND233-367) Answering machine detection: status `OUTGOING_CALL_ANSWERING_MACHINE_DETECTED = 22` (not terminal), `AnsweringMachineDetectionResult` (verdict, cause, confidence, decision time, rule and cue ids, action taken, call id), `SipStatus.amd_result` (field 11), `SipEndCallRequest.end_reason` with `ANSWERING_MACHINE` / `ANSWERING_MACHINE_VOICE_MESSAGE_LEFT` and `SipEndCallRequest.amd_result`, and the in-container `SipReportAnsweringMachineDetected` RPC.
* [[OND233-367]](https://ondewo.atlassian.net/browse/OND233-367) Call identity: `SipStatus.call_id` (field 12), minted per call from `X-ondewo-vtsi-caller-call-id` or a random UUID. Clients scope a request to the call with the `x-ondewo-expected-call-id` gRPC metadatum; a present but different value is refused (`CallScopeMismatch`) on `SipTransferCall`, `SipMute`, `SipUnMute` and `SipPlayWavFiles`, and required on the new RPCs.
* [[OND233-367]](https://ondewo.atlassian.net/browse/OND233-367) `SipSetCallMediaControl`: call-scoped operator media control (mute the bot, pause its listening) as per-owner holds (`MediaControlSetting`, `MediaControlOwner`, `SipSetCallMediaControlRequest`). Requires the `x-ondewo-expected-call-id` and `x-ondewo-sip-call-control-token` metadata. The effective level is reported in `SipStatus.bot_muted` (13) and `SipStatus.listening_paused` (14).
* [[OND233-367]](https://ondewo.atlassian.net/browse/OND233-367) `SipSetCallMediaControlRequest.participants_present` (field 4, participant owner only): while invited participants ring or are joined, `SipTransferCall` is refused with `exception_name=ParticipantsPresent` (`reason=participants-present`), because a REFER into a conference bridge transfers every party in it. Marking participants present while a transfer is in flight is refused with `TransferInProgress`.
* [[OND233-367]](https://ondewo.atlassian.net/browse/OND233-367) `SipStreamCallAudio`: bidirectional live call audio (LISTEN, or TALK with a mandatory bot take-over), LINEAR16 mono 20 ms frames at 8 or 16 kHz (`SipCallAudioConfig`, `SipCallAudioFrame`, `SipCallAudioRequest`, `SipCallAudioResponse`, `SipCallAudioStarted`, `SipCallAudioStats`, `SipCallAudioEnded`, `SipCallAudioMode`, `SipCallAudioEndReason`). Connected streams are counted in `SipStatus.call_audio_streams` (15).
* [[OND233-367]](https://ondewo.atlassian.net/browse/OND233-367) Truthful transfers: `SipTransferCallRequest.outcome_timeout_ms` (field 3). `0` keeps the legacy REFER-then-hangup flow; a positive value waits for the REFER outcome, keeps the call on a refusal or timeout and reports the SIP code in `SipStatus.sip_response_code` (16). New `SipEndCallRequest.EndCallReason.END_CALL_REASON_TRANSFERRED = 3` for a completed WARM transfer; the call then ends as `*_CALL_FINISHED` with the description `Call transferred`.

### Improvements

* Documented that Asterisk does not forward the headers of a REFER to the transfer target.
* Purely additive: no field, enum value or RPC was renumbered or removed, and no `SipStatus.StatusType` value was added beyond the answering machine status, so a client built against 5.4.0 stays wire-compatible.

*****************

## Release ONDEWO SIP API 5.4.0

### Improvements

* [[OND211-2418]](https://ondewo.atlassian.net/browse/OND211-2418) Added Jenkins multibranch-scan guidance in CLAUDE.md and fixed pre-commit hook order for conventional commit validation

*****************

## Release ONDEWO SIP API 5.3.0

### Improvements

* Added async support to SIP API client [[5.2.0]](

*****************

## Release ONDEWO SIP API 5.2.0

### Improvements

* Updated SIP clients to ONDEWO Proto
  Compiler [[5.2.0]](https://github.com/ondewo/ondewo-proto-compiler/releases/tag/5.2.0)

*****************

## Release ONDEWO SIP API 5.1.0

### Improvements

* [[OND236-35]](https://ondewo.atlassian.net/browse/OND236-35) Added nlu_session_name to SipStatus

*****************

## Release ONDEWO SIP API 5.0.0

### Improvements

* Prefix endpoints with "Sip"

*****************

## Release ONDEWO SIP API 4.0.0

### Improvements

* Synchronize API Client Versions

*****************

## Release ONDEWO SIP API 3.3.0

### New Features

* Added further SipStatus states including description and exception details as fields
* [[OND236-20]](https://ondewo.atlassian.net/browse/OND236-20) Refactor SIP and provide better API interfaces and
  documentation

*****************

## Release ONDEWO SIP API 3.2.0

### New Features

* [[OND236-20]](https://ondewo.atlassian.net/browse/OND236-20) Refactor SIP and provide better API interfaces and
  documentation

*****************

## Release ONDEWO SIP API 3.1.0

### New Features

* [[OND211-2039]](https://ondewo.atlassian.net/browse/OND211-2039) Added pre-commit hooks and adjusted files to them

*****************

## Release ONDEWO SIP API 3.0.0

### New Features

* [[OND211-2039]](https://ondewo.atlassian.net/browse/OND211-2039) Automated release process

*****************

## Release ONDEWO SIP API 1.2.0

### New Features

* added muting and unmuting

*****************

## Release ONDEWO SIP API 1.1.0

### New Features

* added a map in calls or transfers which support extra headers
