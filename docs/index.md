# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [ondewo/sip/sip.proto](#ondewo/sip/sip.proto)
    - [AnsweringMachineDetectionResult](#ondewo.sip.AnsweringMachineDetectionResult)
    - [SipCallAudioConfig](#ondewo.sip.SipCallAudioConfig)
    - [SipCallAudioEnded](#ondewo.sip.SipCallAudioEnded)
    - [SipCallAudioFrame](#ondewo.sip.SipCallAudioFrame)
    - [SipCallAudioRequest](#ondewo.sip.SipCallAudioRequest)
    - [SipCallAudioResponse](#ondewo.sip.SipCallAudioResponse)
    - [SipCallAudioStarted](#ondewo.sip.SipCallAudioStarted)
    - [SipCallAudioStats](#ondewo.sip.SipCallAudioStats)
    - [SipDelegatedTransfer](#ondewo.sip.SipDelegatedTransfer)
    - [SipDelegatedTransfer.HeadersEntry](#ondewo.sip.SipDelegatedTransfer.HeadersEntry)
    - [SipEndCallRequest](#ondewo.sip.SipEndCallRequest)
    - [SipPlayWavFilesRequest](#ondewo.sip.SipPlayWavFilesRequest)
    - [SipRegisterAccountRequest](#ondewo.sip.SipRegisterAccountRequest)
    - [SipReportAnsweringMachineDetectedRequest](#ondewo.sip.SipReportAnsweringMachineDetectedRequest)
    - [SipSendDtmfRequest](#ondewo.sip.SipSendDtmfRequest)
    - [SipSetCallMediaControlRequest](#ondewo.sip.SipSetCallMediaControlRequest)
    - [SipStartCallRequest](#ondewo.sip.SipStartCallRequest)
    - [SipStartCallRequest.HeadersEntry](#ondewo.sip.SipStartCallRequest.HeadersEntry)
    - [SipStartSessionRequest](#ondewo.sip.SipStartSessionRequest)
    - [SipStatus](#ondewo.sip.SipStatus)
    - [SipStatus.HeadersEntry](#ondewo.sip.SipStatus.HeadersEntry)
    - [SipStatusHistoryResponse](#ondewo.sip.SipStatusHistoryResponse)
    - [SipTransferCallRequest](#ondewo.sip.SipTransferCallRequest)
    - [SipTransferCallRequest.HeadersEntry](#ondewo.sip.SipTransferCallRequest.HeadersEntry)
    - [SipWarmTransferOutcomeNotice](#ondewo.sip.SipWarmTransferOutcomeNotice)
  
    - [AnsweringMachineDetectionResult.ActionTaken](#ondewo.sip.AnsweringMachineDetectionResult.ActionTaken)
    - [AnsweringMachineDetectionResult.Cause](#ondewo.sip.AnsweringMachineDetectionResult.Cause)
    - [AnsweringMachineDetectionResult.Verdict](#ondewo.sip.AnsweringMachineDetectionResult.Verdict)
    - [MediaControlOwner](#ondewo.sip.MediaControlOwner)
    - [MediaControlSetting](#ondewo.sip.MediaControlSetting)
    - [SipCallAudioEndReason](#ondewo.sip.SipCallAudioEndReason)
    - [SipCallAudioMode](#ondewo.sip.SipCallAudioMode)
    - [SipEndCallRequest.EndCallReason](#ondewo.sip.SipEndCallRequest.EndCallReason)
    - [SipStatus.StatusType](#ondewo.sip.SipStatus.StatusType)
    - [SipTransferDelegation](#ondewo.sip.SipTransferDelegation)
    - [SipWarmTransferOutcome](#ondewo.sip.SipWarmTransferOutcome)
    - [SipWarmTransferOutcomeNoticeStatus](#ondewo.sip.SipWarmTransferOutcomeNoticeStatus)
  
    - [Sip](#ondewo.sip.Sip)
  
- [Scalar Value Types](#scalar-value-types)



<a name="ondewo/sip/sip.proto"></a>
<p align="right"><a href="#top">Top</a></p>

## ondewo/sip/sip.proto



<a name="ondewo.sip.AnsweringMachineDetectionResult"></a>

### AnsweringMachineDetectionResult
<p>Result of the answering machine detection (AMD) of an outbound call</p>
<p>Carries identifiers from closed vocabularies only: never audio, transcript text or a phone number</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| verdict | [AnsweringMachineDetectionResult.Verdict](#ondewo.sip.AnsweringMachineDetectionResult.Verdict) |  | Who or what answered the call |
| cause | [AnsweringMachineDetectionResult.Cause](#ondewo.sip.AnsweringMachineDetectionResult.Cause) |  | Evidence that led to the verdict |
| confidence | [float](#float) |  | Confidence of the verdict, between <code>0.0</code> and <code>1.0</code> |
| decision_ms | [int32](#int32) |  | Time in milliseconds from the call being connected until the verdict was reached |
| rule_id | [string](#string) |  | Identifier of the detection rule that produced the verdict |
| matched_cue_ids | [string](#string) | repeated | Identifiers of the cues that matched, e.g. keyword or tone identifiers. Identifiers only, never transcript text |
| action_taken | [AnsweringMachineDetectionResult.ActionTaken](#ondewo.sip.AnsweringMachineDetectionResult.ActionTaken) |  | What was done because of the verdict |
| call_id | [string](#string) |  | Identifier of the call the result belongs to, i.e. the value of the <code>X-ondewo-vtsi-caller-call-id</code> header of the call. Used to match a result to its call by identity rather than by recency |






<a name="ondewo.sip.SipCallAudioConfig"></a>

### SipCallAudioConfig
<p>Configuration of a <code>SipStreamCallAudio</code> stream. Must be the first request of the stream</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| mode | [SipCallAudioMode](#ondewo.sip.SipCallAudioMode) |  | Mode of the stream. Unspecified means LISTEN |
| sample_rate_hz | [int32](#int32) |  | Sample rate in Hz of the audio in both directions: <code>8000</code> or <code>16000</code>. <code>0</code> means <code>16000</code> |
| frame_ms | [int32](#int32) |  | Frame length in milliseconds. Only <code>20</code> is supported; <code>0</code> means <code>20</code> |
| take_over | [bool](#bool) |  | REQUIRED for TALK: the bot is muted and does not listen while the stream is connected. Released when the stream ends |
| stream_id | [string](#string) |  | Identifier of the stream for logs and audit correlation, minted by the client (a UUID) |
| max_duration_s | [int32](#int32) |  | Maximum duration of the stream in seconds. <code>0</code> means the server default (3600) |






<a name="ondewo.sip.SipCallAudioEnded"></a>

### SipCallAudioEnded
<p>Sent once when a <code>SipStreamCallAudio</code> stream ends normally</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| reason | [SipCallAudioEndReason](#ondewo.sip.SipCallAudioEndReason) |  | Why the stream ended |
| detail | [string](#string) |  | Optional detail, a stable token |






<a name="ondewo.sip.SipCallAudioFrame"></a>

### SipCallAudioFrame
<p>One frame of call audio</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| pcm_s16le | [bytes](#bytes) |  | LINEAR16 little-endian mono samples of one frame, i.e. <code>sample_rate_hz * frame_ms / 1000 * 2</code> bytes |
| sequence | [uint64](#uint64) |  | Monotonic sequence number of the frame within its direction of the stream |






<a name="ondewo.sip.SipCallAudioRequest"></a>

### SipCallAudioRequest
<p>Request of <code>SipStreamCallAudio</code></p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| config | [SipCallAudioConfig](#ondewo.sip.SipCallAudioConfig) |  | Configuration; must be the first request and is accepted only once |
| audio | [SipCallAudioFrame](#ondewo.sip.SipCallAudioFrame) |  | Agent audio to send to the caller (TALK only) |
| agent_muted | [bool](#bool) |  | <code>true</code>: the agent's audio is not sent to the caller (silence instead) until set to <code>false</code> |






<a name="ondewo.sip.SipCallAudioResponse"></a>

### SipCallAudioResponse
<p>Response of <code>SipStreamCallAudio</code></p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| started | [SipCallAudioStarted](#ondewo.sip.SipCallAudioStarted) |  | The stream is connected |
| audio | [SipCallAudioFrame](#ondewo.sip.SipCallAudioFrame) |  | Call audio |
| stats | [SipCallAudioStats](#ondewo.sip.SipCallAudioStats) |  | Stream counters |
| ended | [SipCallAudioEnded](#ondewo.sip.SipCallAudioEnded) |  | The stream ended |






<a name="ondewo.sip.SipCallAudioStarted"></a>

### SipCallAudioStarted
<p>Sent once when a <code>SipStreamCallAudio</code> stream is connected</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| stream_id | [string](#string) |  | Identifier of the stream |
| sample_rate_hz | [int32](#int32) |  | Sample rate in Hz of the audio in both directions |
| frame_ms | [int32](#int32) |  | Frame length in milliseconds |
| mode | [SipCallAudioMode](#ondewo.sip.SipCallAudioMode) |  | Mode of the stream |






<a name="ondewo.sip.SipCallAudioStats"></a>

### SipCallAudioStats
<p>Counters of a <code>SipStreamCallAudio</code> stream, sent periodically</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| frames_sent | [uint64](#uint64) |  | Frames sent to the client |
| frames_dropped | [uint64](#uint64) |  | Frames to the client dropped because the client read too slowly |
| frames_received | [uint64](#uint64) |  | Frames received from the client |
| underruns | [uint64](#uint64) |  | Playback underruns of the agent audio (silence was played) |
| frames_discarded | [uint64](#uint64) |  | Frames from the client discarded because the playback buffer was full |






<a name="ondewo.sip.SipDelegatedTransfer"></a>

### SipDelegatedTransfer
<p>A transfer that the in-container speech-to-speech pipeline asked for and the container handed to a client instead
of sending it (see <code>SipTransferDelegation</code>). Call-scoped: empty when no transfer is parked, when no call
is ongoing, and after the call ended.</p>
<p><code>SipGetSipStatus</code>, <code>SipGetSipStatusHistory</code> and every other response report only
<code>request_id</code>, <code>requested_at</code> and <code>target_is_phone_number</code>. The target and the headers
are filled ONLY in the response of a <code>SIP_TRANSFER_DELEGATION_CLAIM</code>.</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| request_id | [string](#string) |  | Identifier of the parked transfer, a UUID minted by ONDEWO SIP. Sent back as <code>SipTransferCallRequest.delegated_request_id</code>. Empty when no transfer is parked |
| requested_at | [google.protobuf.Timestamp](#google.protobuf.Timestamp) |  | When the pipeline asked for the transfer |
| target_is_phone_number | [bool](#bool) |  | <code>true</code> when the target is a phone number by the transfer target policy of ONDEWO SIP (a leading <code>+</code> followed by digits, or a trunk-routed number), <code>false</code> for an account name such as a softphone |
| transfer_id | [string](#string) |  | The target the pipeline asked for, already checked by the transfer target policy. Only in the response of a <code>SIP_TRANSFER_DELEGATION_CLAIM</code>, empty everywhere else |
| headers | [SipDelegatedTransfer.HeadersEntry](#ondewo.sip.SipDelegatedTransfer.HeadersEntry) | repeated | The headers the pipeline sent with the transfer. Only in the response of a <code>SIP_TRANSFER_DELEGATION_CLAIM</code>, empty everywhere else |






<a name="ondewo.sip.SipDelegatedTransfer.HeadersEntry"></a>

### SipDelegatedTransfer.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="ondewo.sip.SipEndCallRequest"></a>

### SipEndCallRequest
<p>Ends an ongoing call of the active SIP session of the active SIP account</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hard_hangup | [bool](#bool) |  | Set to <code>True</code> to forcefully hang up the call |
| end_reason | [SipEndCallRequest.EndCallReason](#ondewo.sip.SipEndCallRequest.EndCallReason) |  | Optional: reason for ending the call. Leave unset for an ordinary hangup |
| amd_result | [AnsweringMachineDetectionResult](#ondewo.sip.AnsweringMachineDetectionResult) |  | Optional: result of the answering machine detection that decided to end the call. Only meaningful together with <code>end_reason = ANSWERING_MACHINE</code> or <code>end_reason = ANSWERING_MACHINE_VOICE_MESSAGE_LEFT</code>; it is carried into <code>SipStatus.amd_result</code> of the terminal status of the call |






<a name="ondewo.sip.SipPlayWavFilesRequest"></a>

### SipPlayWavFilesRequest
<p>Plays a list of wav files</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| wav_files | [bytes](#bytes) | repeated | Wav files as bytes in a list that will be played |






<a name="ondewo.sip.SipRegisterAccountRequest"></a>

### SipRegisterAccountRequest
<p>Request for registering a SIP account at a SIP server</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  | Account name of the sip user. Usually something like <code>sip-user-1@mydomain.com</code> or <code>sip-user-1@192.168.123.123</code> which uses the default SIP port <code>5060</code>. Also a non-default SIP port can be specified via <code>sip-user-1@mydomain.com:5099</code> to connect to a SIP server running on port <code>5099</code> |
| password | [string](#string) |  | Password of the account |
| auth_username | [string](#string) |  | Optional: authentication user name |
| outbound_proxy | [string](#string) |  | Optional: outbound proxy address, e.g. <code>my.outbound.proxy.com</code> |






<a name="ondewo.sip.SipReportAnsweringMachineDetectedRequest"></a>

### SipReportAnsweringMachineDetectedRequest
<p>Reports the verdict of the answering machine detection of the ongoing outgoing call</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| amd_result | [AnsweringMachineDetectionResult](#ondewo.sip.AnsweringMachineDetectionResult) |  | Result of the answering machine detection. Written to <code>SipStatus.amd_result</code> of the <code>OUTGOING_CALL_ANSWERING_MACHINE_DETECTED</code> status of the call |






<a name="ondewo.sip.SipSendDtmfRequest"></a>

### SipSendDtmfRequest
<p>Request of <code>SipSendDtmf</code></p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| digits | [string](#string) |  | The keys to send, in order: <code>0</code>-<code>9</code>, <code>*</code>, <code>#</code>, <code>A</code>-<code>D</code>; at most 64. Any other character refuses the request (<code>InvalidDtmf</code>) and sends nothing |






<a name="ondewo.sip.SipSetCallMediaControlRequest"></a>

### SipSetCallMediaControlRequest
<p>Request of <code>SipSetCallMediaControl</code></p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| bot_voice | [MediaControlSetting](#ondewo.sip.MediaControlSetting) |  | <code>MEDIA_CONTROL_SETTING_ON</code>: the bot speaks. <code>MEDIA_CONTROL_SETTING_OFF</code>: the bot is muted |
| bot_listening | [MediaControlSetting](#ondewo.sip.MediaControlSetting) |  | <code>MEDIA_CONTROL_SETTING_ON</code>: caller audio reaches speech-to-text. <code>MEDIA_CONTROL_SETTING_OFF</code>: listening is paused |
| owner | [MediaControlOwner](#ondewo.sip.MediaControlOwner) |  | Owner whose hold is set |
| participants_present | [bool](#bool) |  | <p>Only for <code>MEDIA_CONTROL_OWNER_PARTICIPANT</code>, ignored for every other owner: whether at least one invited participant is ringing or joined. Every participant request carries the full value, so the request that reports the last participant gone sends <code>false</code>.</p> <p>While participants are present (this flag, or a mute or pause held by the participant owner) <code>SipTransferCall</code> is refused with <code>exception_name=ParticipantsPresent</code>, because a REFER into a conference bridge transfers every party in it. A request that would mark participants present while a transfer of the call is in flight is refused with <code>exception_name=TransferInProgress</code> and changes nothing. Cleared when the call ends</p> |
| warm_transfer_outcome | [SipWarmTransferOutcomeNotice](#ondewo.sip.SipWarmTransferOutcomeNotice) |  | <p>Optional, only with <code>MEDIA_CONTROL_OWNER_PARTICIPANT</code> (any other owner, an outcome other than <code>SIP_WARM_TRANSFER_OUTCOME_DECLINED</code> / <code>SIP_WARM_TRANSFER_OUTCOME_UNREACHABLE</code>, or an empty <code>request_id</code> is refused with <code>exception_name=InvalidWarmTransferOutcomeNotice</code> and changes nothing). The outcome of a warm transfer that the bot must tell the caller, sent with the request that releases the participant hold, so the bot speaks only once it can.</p> <p>Handed to the speech-to-speech pipeline after the level, also when the level did not change; the answer is returned in <code>SipStatus.warm_transfer_outcome_notice_status</code>. A notice the pipeline did not answer is kept and handed over again until it answers, and dropped when the call ends. Unset (default): no notice, exactly as before this field existed.</p> |






<a name="ondewo.sip.SipStartCallRequest"></a>

### SipStartCallRequest
<p>Request to start the call with the active SIP session of the active SIP account</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| callee_id | [string](#string) |  | SIP account name |
| headers | [SipStartCallRequest.HeadersEntry](#ondewo.sip.SipStartCallRequest.HeadersEntry) | repeated | Headers to include when starting the call |






<a name="ondewo.sip.SipStartCallRequest.HeadersEntry"></a>

### SipStartCallRequest.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="ondewo.sip.SipStartSessionRequest"></a>

### SipStartSessionRequest
<p>Request for starting a new SIP session for a specified account</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  | Account name of the sip user. Usually something like <code>sip-user-1@mydomain.com</code> or <code>sip-user-1@192.168.123.123</code> which uses the default SIP port <code>5060</code>. Also a non-default SIP port can be specified via <code>sip-user-1@mydomain.com:5099</code> to connect to a SIP server running on port <code>5099</code> |
| auto_answer_interval | [int32](#int32) |  | Auto-answer interval in seconds. The call will be automatically answered after this interval |






<a name="ondewo.sip.SipStatus"></a>

### SipStatus
<p>Status information for a SIP account, session, or call</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  | Account name of the sip user. Usually something like <code>sip-user-1@mydomain.com</code> or <code>sip-user-1@192.168.123.123</code> which uses the default SIP port <code>5060</code>. Also a non-default SIP port can be specified via <code>sip-user-1@mydomain.com:5099</code> to connect to a SIP server running on port <code>5099</code> |
| timestamp | [google.protobuf.Timestamp](#google.protobuf.Timestamp) |  | Timestamp of the status |
| status_type | [SipStatus.StatusType](#ondewo.sip.SipStatus.StatusType) |  | Status type |
| callee_id | [string](#string) |  | SIP account name |
| transfer_call_id | [string](#string) |  | SIP account of the transfer |
| headers | [SipStatus.HeadersEntry](#ondewo.sip.SipStatus.HeadersEntry) | repeated | Headers to include when calling outbound or transfer |
| description | [string](#string) |  | More detailed description of the status |
| exception_name | [string](#string) |  | Name of the exception |
| exception_traceback | [string](#string) |  | Traceback of the exception |
| nlu_session_name | [string](#string) |  | session name of the NLU session |
| amd_result | [AnsweringMachineDetectionResult](#ondewo.sip.AnsweringMachineDetectionResult) |  | Result of the answering machine detection of the call. Set on <code>OUTGOING_CALL_ANSWERING_MACHINE_DETECTED</code> and on the terminal status of every call on which answering machine detection ran, including a <code>HUMAN</code> verdict; unset otherwise |
| call_id | [string](#string) |  | Identifier of the ongoing call, minted per call: the value of the <code>X-ondewo-vtsi-caller-call-id</code> header of an outgoing call when present, otherwise a random UUID. Empty when no call is ongoing. Set on every status of the call, including the entries of <code>SipGetSipStatusHistory</code>. Clients send it back as the <code>x-ondewo-expected-call-id</code> metadatum to scope a request to this call |
| bot_muted | [bool](#bool) |  | <code>true</code> while the bot is muted by an operator, a conference participant policy or a TALK take-over of <code>SipSetCallMediaControl</code> / <code>SipStreamCallAudio</code>. Not the bot's own pipeline mute (<code>MICROPHONE_MUTED</code>). Cleared when the call ends |
| listening_paused | [bool](#bool) |  | <code>true</code> while the bot does not listen to the caller (see <code>bot_muted</code> for who sets it). Cleared when the call ends |
| call_audio_streams | [int32](#int32) |  | Number of connected <code>SipStreamCallAudio</code> streams of the ongoing call |
| sip_response_code | [int32](#int32) |  | SIP response code of the last transfer attempt of the ongoing call (<code>202</code> when accepted, the refusal code otherwise, <code>0</code> when unknown). Call-scoped |
| delegated_transfer | [SipDelegatedTransfer](#ondewo.sip.SipDelegatedTransfer) |  | The transfer parked for a client to claim (see <code>SipTransferDelegation</code>). Unset (empty) when no transfer is parked, which is always the case in a container started without <code>SIP_TRANSFER_DELEGATION_ACTIVE=True</code>. Call-scoped |
| capabilities | [string](#string) | repeated | <p>Optional features this container supports, as stable tokens. Fixed for the life of the container, so it is the same on every status. Empty (default): none of them, as for a container built before this field existed. Clients ignore tokens they do not know.</p> <ul> <li><code>warm-transfer-outcome-notice</code>: <code>SipSetCallMediaControlRequest.warm_transfer_outcome</code> is handed to the speech-to-speech pipeline, and the pipeline tells the caller.</li> </ul> |
| warm_transfer_outcome_notice_status | [SipWarmTransferOutcomeNoticeStatus](#ondewo.sip.SipWarmTransferOutcomeNoticeStatus) |  | Answer of the speech-to-speech pipeline to the <code>warm_transfer_outcome</code> notice of a <code>SipSetCallMediaControl</code> request. Only in the response of that request; <code>SIP_WARM_TRANSFER_OUTCOME_NOTICE_STATUS_UNSPECIFIED</code> everywhere else and when the request carried no notice |






<a name="ondewo.sip.SipStatus.HeadersEntry"></a>

### SipStatus.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="ondewo.sip.SipStatusHistoryResponse"></a>

### SipStatusHistoryResponse
<p>History of SIP status</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| status_history | [SipStatus](#ondewo.sip.SipStatus) | repeated | History of SIP status |






<a name="ondewo.sip.SipTransferCallRequest"></a>

### SipTransferCallRequest
<p>Request for transferring a call with or without headers</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| transfer_id | [string](#string) |  | The account name or phone number to transfer the call to |
| headers | [SipTransferCallRequest.HeadersEntry](#ondewo.sip.SipTransferCallRequest.HeadersEntry) | repeated | The headers to include when transferring the call. They are sent on the REFER. Note that Asterisk (res_pjsip, measured on 18.6 and 22) does NOT forward headers of a REFER to the transfer target: the target receives the headers of the transferred caller's original INVITE. Hand headers to the target through the dialplan instead |
| outcome_timeout_ms | [uint32](#uint32) |  | <p>Optional. How long to wait, in milliseconds, for the SIP server's answer to the REFER before reporting the outcome. Clamped to 10000.</p> <p><code>0</code> (default): legacy behaviour, unchanged: REFER, then an immediate hangup.</p> <p><code>&gt; 0</code>: the call is kept until the outcome is known:</p> <ul> <li>REFER accepted (<code>202</code>): the hangup is held for a short grace in which a terminal NOTIFY with a <code>404</code> sipfrag (unknown target) still counts as a refusal; any other sipfrag, or none, means accepted. The bot then hangs up and <code>TRANSFER_CALL_INITIATED</code> is returned with <code>sip_response_code = 202</code>. The call ends as <code>*_CALL_FINISHED</code> with the description <code>Call transferred</code>.</li> <li>REFER refused (a final response <code>&gt;= 400</code>, or the <code>404</code> sipfrag above): the call is KEPT with the bot, nothing is assigned to the shared status, and <code>TRANSFER_CALL_FAILED</code> is returned with <code>description = reason=refer-rejected</code> and <code>sip_response_code</code> (<code>0</code> when the SIP stack did not report the code, e.g. a declined REFER).</li> <li>No answer within the timeout: the call is KEPT and <code>TRANSFER_CALL_FAILED</code> is returned with <code>description = reason=refer-timeout</code>. A late acceptance still ends the bot's leg.</li> <li>The call ended while waiting: <code>NO_ONGOING_CALL</code> is returned.</li> </ul> <p>A <code>202</code> does not mean the target answered: when the dialplan's dial to the target then fails (busy, no answer, unreachable) the caller is lost. Validate targets up front, or use a WARM transfer.</p> |
| delegation | [SipTransferDelegation](#ondewo.sip.SipTransferDelegation) |  | <p>Optional. Claims the transfer parked in <code>SipStatus.delegated_transfer</code> (see <code>SipTransferDelegation</code>). <code>SIP_TRANSFER_DELEGATION_UNSPECIFIED</code> (default): an ordinary transfer, exactly as before this field existed.</p> |
| delegated_request_id | [string](#string) |  | <p>Required with every <code>delegation</code> other than <code>SIP_TRANSFER_DELEGATION_UNSPECIFIED</code>, ignored otherwise: must equal <code>SipStatus.delegated_transfer.request_id</code> of the parked transfer, otherwise the request is refused with <code>exception_name=DelegatedRequestMismatch</code> and nothing is sent. Empty (default): no delegated transfer is claimed.</p> |






<a name="ondewo.sip.SipTransferCallRequest.HeadersEntry"></a>

### SipTransferCallRequest.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="ondewo.sip.SipWarmTransferOutcomeNotice"></a>

### SipWarmTransferOutcomeNotice
<p>One-shot notice of a warm-transfer outcome for the bot. The pipeline tells the caller at most once per
<code>request_id</code> and call. Carries no reason text the target gave</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| request_id | [string](#string) |  | Identifier of the transfer request of the client (ONDEWO VTSI). Required; the notice is delivered at most once per call for one identifier |
| outcome | [SipWarmTransferOutcome](#ondewo.sip.SipWarmTransferOutcome) |  | The outcome |
| intro_session | [string](#string) |  | Optional: NLU session name of the session in which the transfer target was introduced, so the pipeline can relay what the target said. Empty when there was no intro |
| callee_display_name | [string](#string) |  | Optional: display name of the transfer target, at most 128 characters |
| cause | [string](#string) |  | Optional: a stable token naming why the transfer did not complete, e.g. <code>target-hung-up</code>, <code>target-refused</code>, <code>voicemail-suspected</code>. Never free text |
| fallback_text | [string](#string) |  | Optional: the sentence the pipeline speaks itself when it cannot have the NLU phrase the outcome, rendered by the client. Never contains a reason the target gave. Empty: the pipeline has no sentence of its own to fall back on |





 <!-- end messages -->


<a name="ondewo.sip.AnsweringMachineDetectionResult.ActionTaken"></a>

### AnsweringMachineDetectionResult.ActionTaken
<p>What was done because of the verdict</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| ACTION_TAKEN_UNSPECIFIED | 0 | No action recorded |
| HUNG_UP | 1 | The call was hung up |
| CONTINUED | 2 | The call continued as normal |
| DETECT_ONLY | 3 | Detection only: the verdict was recorded, but the call was not influenced by it |
| LEFT_VOICE_MESSAGE | 4 | A voice message was left on the answering machine, and the call was hung up afterwards |



<a name="ondewo.sip.AnsweringMachineDetectionResult.Cause"></a>

### AnsweringMachineDetectionResult.Cause
<p>Evidence that led to the verdict</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| CAUSE_UNSPECIFIED | 0 | No cause available |
| CADENCE | 1 | The speech cadence, e.g. a long uninterrupted greeting |
| KEYWORD | 2 | A keyword or phrase typical of the verdict |
| BEEP | 3 | A voicemail beep |
| TONE | 4 | A tone, e.g. a fax or special information tone |
| CADENCE_AND_KEYWORD | 5 | Both the speech cadence and a keyword |
| CADENCE_AND_BEEP | 6 | Both the speech cadence and a voicemail beep |
| TIMEOUT | 7 | The detection window ended before any other evidence decided |
| SILENCE | 8 | Silence throughout the detection window |



<a name="ondewo.sip.AnsweringMachineDetectionResult.Verdict"></a>

### AnsweringMachineDetectionResult.Verdict
<p>Who or what answered the call</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| VERDICT_UNSPECIFIED | 0 | No verdict available |
| HUMAN | 1 | A person answered the call |
| MACHINE | 2 | An answering machine or voicemail answered the call |
| IVR | 3 | An interactive voice response system (IVR) answered the call |
| FAX | 4 | A fax machine answered the call |
| NETWORK_ANNOUNCEMENT | 5 | A network announcement answered the call, e.g. "the number you have dialed is not available" |
| CALL_SCREENING | 6 | A call screening service answered the call, e.g. asking the caller to state their name |
| NO_SPEECH | 7 | Nothing was said within the detection window |
| UNKNOWN | 8 | The detection could not decide |



<a name="ondewo.sip.MediaControlOwner"></a>

### MediaControlOwner
<p>Owner of a media control hold. Each owner holds its own mute and pause; releasing one owner's hold never releases
another owner's</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| MEDIA_CONTROL_OWNER_UNSPECIFIED | 0 | Same as <code>MEDIA_CONTROL_OWNER_OPERATOR</code> |
| MEDIA_CONTROL_OWNER_OPERATOR | 1 | An operator, e.g. a supervisor muting the bot |
| MEDIA_CONTROL_OWNER_PARTICIPANT | 2 | The bot policy of invited conference participants, set while at least one participant is ringing or joined. Its hold mutes or pauses the bot only when a participant's bot policy asks for it; it also carries <code>SipSetCallMediaControlRequest.participants_present</code> |



<a name="ondewo.sip.MediaControlSetting"></a>

### MediaControlSetting
<p>Desired setting of one media control flag</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| MEDIA_CONTROL_SETTING_UNCHANGED | 0 | Leave the flag as it is for this owner |
| MEDIA_CONTROL_SETTING_ON | 1 | The flag is on: the bot speaks (<code>bot_voice</code>) or the bot listens (<code>bot_listening</code>) |
| MEDIA_CONTROL_SETTING_OFF | 2 | The flag is off: the bot is muted (<code>bot_voice</code>) or the bot's listening is paused (<code>bot_listening</code>) |



<a name="ondewo.sip.SipCallAudioEndReason"></a>

### SipCallAudioEndReason
<p>Why a <code>SipStreamCallAudio</code> stream ended</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| SIP_CALL_AUDIO_END_REASON_UNSPECIFIED | 0 | No reason recorded |
| SIP_CALL_AUDIO_END_REASON_CLIENT_CLOSED | 1 | The client cancelled or half-closed the stream |
| SIP_CALL_AUDIO_END_REASON_CALL_ENDED | 2 | The call ended |
| SIP_CALL_AUDIO_END_REASON_CALL_TRANSFERRED | 3 | The call was transferred |
| SIP_CALL_AUDIO_END_REASON_MAX_DURATION | 4 | <code>max_duration_s</code> was reached |
| SIP_CALL_AUDIO_END_REASON_STALLED | 5 | The client did not read the audio in time |
| SIP_CALL_AUDIO_END_REASON_INTERNAL | 6 | An internal error ended the stream |



<a name="ondewo.sip.SipCallAudioMode"></a>

### SipCallAudioMode
<p>Mode of a <code>SipStreamCallAudio</code> stream</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| SIP_CALL_AUDIO_MODE_UNSPECIFIED | 0 | Same as <code>SIP_CALL_AUDIO_MODE_LISTEN</code> |
| SIP_CALL_AUDIO_MODE_LISTEN | 1 | Receive the call audio only |
| SIP_CALL_AUDIO_MODE_TALK | 2 | Receive the caller's audio and send audio to the caller. Requires <code>take_over</code> |



<a name="ondewo.sip.SipEndCallRequest.EndCallReason"></a>

### SipEndCallRequest.EndCallReason
<p>Why the call is being ended</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| END_CALL_REASON_UNSPECIFIED | 0 | No specific reason given. The call ends as an ordinary hangup, exactly as before this field existed |
| ANSWERING_MACHINE | 1 | Answering machine detection decided the callee is not a person to talk to (answering machine, fax, network announcement, ...) and the call is hung up WITHOUT leaving a voice message. The terminal status of the call is <code>OUTGOING_CALL_FINISHED</code> with the description <code>Answering machine detected with hang up</code> |
| ANSWERING_MACHINE_VOICE_MESSAGE_LEFT | 2 | Answering machine detection decided the callee is an answering machine, a voice message was left on it, and the call is hung up afterwards (or when the voice message timeout expired). The terminal status of the call is <code>OUTGOING_CALL_FINISHED</code> with the description <code>Answering machine detected with left voice message and hang up</code> |
| END_CALL_REASON_TRANSFERRED | 3 | A WARM transfer completed: the transfer target joined the call and the bot leaves it. The terminal status of the call is <code>*_CALL_FINISHED</code> with the description <code>Call transferred</code> and <code>transfer_call_id</code> set to the transfer target |



<a name="ondewo.sip.SipStatus.StatusType"></a>

### SipStatus.StatusType
Types of status

| Name | Number | Description |
| ---- | ------ | ----------- |
| NO_SESSION | 0 | No session is currently active |
| REGISTERED | 1 | SIP account is registered at a SIP server |
| READY | 2 | SIP account is ready to call |
| INCOMING_CALL_INITIATED | 3 | SIP account is being called, i.e. inbound/incoming call |
| OUTGOING_CALL_INITIATED | 4 | SIP account starts calling, i.e. outbound/outgoing call |
| OUTGOING_CALL_CONNECTED | 5 | SIP account outbound call is connected |
| INCOMING_CALL_CONNECTED | 6 | SIP account incoming call is connected |
| TRANSFER_CALL_INITIATED | 7 | SIP account starts transferring the call |
| SOFT_HANGUP_INITIATED | 8 | SIP account hangs up the ongoing call |
| HARD_HANGUP_INITIATED | 9 | SIP account forcefully hangs up by terminating the SIP program |
| INCOMING_CALL_FAILED | 10 | SIP account cannot accept the incoming call |
| OUTGOING_CALL_FAILED | 11 | SIP account cannot do an outbound call |
| INCOMING_CALL_FINISHED | 12 | SIP account finished the ongoing incoming call |
| OUTGOING_CALL_FINISHED | 13 | SIP account finished the ongoing outgoing call |
| SESSION_REGISTRATION_FAILED | 14 | Registration of SIP account to SIP server failed |
| SESSION_STARTED | 15 | SIP account started a new SIP session via a SIP server |
| SESSION_ENDED | 16 | SIP account ended active sip session with SIP server |
| TRANSFER_CALL_FAILED | 17 | SIP account cannot transfer the call |
| MICROPHONE_MUTED | 18 | Microphone is muted |
| MICROPHONE_UNMUTED | 19 | Microphone is unmuted |
| MICROPHONE_WAV_FILES_PLAYED | 20 | Microphone has played wav files |
| NO_ONGOING_CALL | 21 | No ongoing call |
| OUTGOING_CALL_ANSWERING_MACHINE_DETECTED | 22 | Answering machine detection decided the callee of the ongoing outgoing call is not a person to talk to. NOT terminal: the call is still up when this status is set. <code>amd_result.verdict</code> tells an answering machine, a fax, a network announcement, ... apart. The call then ends as <code>OUTGOING_CALL_FINISHED</code> carrying <code>amd_result</code> and exactly one of the descriptions <code>Answering machine detected with hang up</code>, <code>Answering machine detected with left voice message and hang up</code>, <code>Answering machine detected, call ended by the answering machine</code> or <code>Answering machine detected, call ended by the answering machine after leaving a voice message</code> |



<a name="ondewo.sip.SipTransferDelegation"></a>

### SipTransferDelegation
<p>How a <code>SipTransferCall</code> handles a transfer that the container parked in
<code>SipStatus.delegated_transfer</code> instead of sending it.</p>
<p>Every value other than <code>SIP_TRANSFER_DELEGATION_UNSPECIFIED</code> requires the
<code>x-ondewo-sip-call-control-token</code> metadatum (otherwise <code>CallControlUnauthenticated</code>) and the
<code>x-ondewo-expected-call-id</code> metadatum naming the ongoing call (missing or different:
<code>CallScopeMismatch</code>), plus <code>delegated_request_id</code> (otherwise
<code>DelegatedRequestMismatch</code>). Refusals are RETURNED in <code>exception_name</code> /
<code>description</code> and never assigned to the shared status.</p>
<p>A parked transfer that is neither claimed nor ended within <code>SIP_TRANSFER_DELEGATION_CLAIM_TIMEOUT_S</code> is
dropped WITHOUT a REFER, and the pipeline is told with <code>SIP_WARM_TRANSFER_OUTCOME_DELEGATION_EXPIRED</code>. A
claimed transfer never expires.</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| SIP_TRANSFER_DELEGATION_UNSPECIFIED | 0 | No delegated transfer is claimed: the request is an ordinary transfer, exactly as before this field existed |
| SIP_TRANSFER_DELEGATION_CLAIM | 1 | Claim the parked transfer and send nothing. The response carries the full target and headers in <code>SipStatus.delegated_transfer.transfer_id</code> / <code>headers</code>, and the parked transfer no longer expires. It stays parked until <code>SIP_TRANSFER_DELEGATION_EXECUTE</code>, <code>SIP_TRANSFER_DELEGATION_DISCARD</code> or the end of the call. A repeated claim answers the same |
| SIP_TRANSFER_DELEGATION_EXECUTE | 2 | End the delegation and send the transfer of THIS request (<code>transfer_id</code>, <code>headers</code>, <code>outcome_timeout_ms</code>) as an ordinary <code>SipTransferCall</code>, with the same outcomes and refusals |
| SIP_TRANSFER_DELEGATION_DISCARD | 3 | End the delegation and send nothing; the call stays with the bot, e.g. because the client handles the transfer itself (a warm transfer with an intro) |



<a name="ondewo.sip.SipWarmTransferOutcome"></a>

### SipWarmTransferOutcome
<p>Outcome of a warm transfer that the bot tells the caller</p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| SIP_WARM_TRANSFER_OUTCOME_UNSPECIFIED | 0 | No outcome |
| SIP_WARM_TRANSFER_OUTCOME_DECLINED | 1 | The transfer target declined the call; the caller stays with the bot |
| SIP_WARM_TRANSFER_OUTCOME_UNREACHABLE | 2 | The transfer target could not be reached: busy, no answer, no decision, or no intro possible; the caller stays with the bot |
| SIP_WARM_TRANSFER_OUTCOME_DELEGATION_EXPIRED | 3 | A transfer parked in <code>SipStatus.delegated_transfer</code> was not claimed in time and was dropped without a REFER. Set by ONDEWO SIP itself towards the pipeline, never accepted from a client |



<a name="ondewo.sip.SipWarmTransferOutcomeNoticeStatus"></a>

### SipWarmTransferOutcomeNoticeStatus
<p>Answer of the speech-to-speech pipeline to a <code>SipWarmTransferOutcomeNotice</code></p>

| Name | Number | Description |
| ---- | ------ | ----------- |
| SIP_WARM_TRANSFER_OUTCOME_NOTICE_STATUS_UNSPECIFIED | 0 | No notice was carried |
| SIP_WARM_TRANSFER_OUTCOME_NOTICE_STATUS_QUEUED | 1 | The pipeline accepted the notice and will tell the caller, unless the call ends first |
| SIP_WARM_TRANSFER_OUTCOME_NOTICE_STATUS_DUPLICATE | 2 | The pipeline already has a notice with this <code>request_id</code> on this call; nothing new is told |
| SIP_WARM_TRANSFER_OUTCOME_NOTICE_STATUS_DISABLED | 3 | The pipeline does not tell the caller about warm-transfer outcomes (switched off); the notice is dropped |
| SIP_WARM_TRANSFER_OUTCOME_NOTICE_STATUS_INVALID | 4 | The pipeline refused the notice as malformed; the notice is dropped |
| SIP_WARM_TRANSFER_OUTCOME_NOTICE_STATUS_PENDING | 5 | The pipeline did not answer (unreachable, or an older pipeline without the notice). The notice is kept and handed over again until it answers or the call ends |


 <!-- end enums -->

 <!-- end HasExtensions -->


<a name="ondewo.sip.Sip"></a>

### Sip
<p>ONDEWO-SIP API available at <a href="https://github.com/ondewo/ondewo-sip-api">GitHub</a></p>

<p>SIP LifeCycle is explained at <a href="https://thanhloi2603.wordpress.com/2017/06/10/sip-lifecycle-overview/">here</a></p>

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| SipStartSession | [SipStartSessionRequest](#ondewo.sip.SipStartSessionRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Starts a new SIP session for an account registered at a SIP server. <code>RegisterAccount</code> need to be called before.</p>

Not idempotent (no idempotency_level): (re)creates the SIP session and registration. |
| SipEndSession | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | <p>Ends a SIP session for an account registered at a SIP server</p>

Not idempotent (no idempotency_level): tears down the session; a repeat records a new status. |
| SipStartCall | [SipStartCallRequest](#ondewo.sip.SipStartCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Starts a call in an active SIP session for an account registered at a SIP server</p>

Not idempotent (no idempotency_level): a repeat dials a second call. |
| SipEndCall | [SipEndCallRequest](#ondewo.sip.SipEndCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Ends a call in an active SIP session for an account registered at a SIP server</p>

Not idempotent (no idempotency_level): a repeat without a call appends its refusal to the history and ends a one-shot caller container; unscoped it can end the next call. |
| SipTransferCall | [SipTransferCallRequest](#ondewo.sip.SipTransferCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Transfers a call in an active SIP session for an account registered at a SIP server to another SIP account or phone number specified by <code>transfer_id</code></p> <p>Call scoping: when the gRPC metadatum <code>x-ondewo-expected-call-id</code> is present it must equal <code>SipStatus.call_id</code> of the ongoing call, otherwise the request is refused with <code>exception_name=CallScopeMismatch</code> and nothing is assigned to the status. When it is absent the request is accepted for backward compatibility (unless the server requires call scoping).</p> <p>With <code>outcome_timeout_ms = 0</code> the call is transferred as before (REFER, then an immediate hangup). With <code>outcome_timeout_ms &gt; 0</code> see <code>SipTransferCallRequest.outcome_timeout_ms</code>.</p> <p>Refused while invited participants are present (see <code>SipSetCallMediaControlRequest.participants_present</code>): a REFER into a conference bridge transfers every party in it, the invited participant included. The refusal is RETURNED as <code>TRANSFER_CALL_FAILED</code> with <code>exception_name=ParticipantsPresent</code> and <code>description = reason=participants-present</code>; nothing is sent and the call is kept.</p> <p>Transfer delegation (see <code>SipTransferDelegation</code>): in a container started with <code>SIP_TRANSFER_DELEGATION_ACTIVE=True</code> a transfer that the in-container speech-to-speech pipeline asks for on a connected call is not sent. It is parked in <code>SipStatus.delegated_transfer</code> and RETURNED as <code>TRANSFER_CALL_FAILED</code> with <code>exception_name=TransferDelegated</code> and <code>description = reason=delegated-to-vtsi</code>; the call is kept. A client (ONDEWO VTSI) then claims it with <code>delegation</code> and <code>delegated_request_id</code>. A second transfer of the pipeline while one is parked is refused with <code>exception_name=TransferInProgress</code>. Without that environment variable, and for every request with <code>delegation = SIP_TRANSFER_DELEGATION_UNSPECIFIED</code> from any other peer, the transfer is sent as before.</p>

Not idempotent (no idempotency_level): a repeat sends another REFER. |
| SipRegisterAccount | [SipRegisterAccountRequest](#ondewo.sip.SipRegisterAccountRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Registers s SIP account at a SIP server</p>

Not idempotent (no idempotency_level): re-registers the account at the SIP server. |
| SipGetSipStatus | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | <p>Gets the current SIP status</p> |
| SipGetSipStatusHistory | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatusHistoryResponse](#ondewo.sip.SipStatusHistoryResponse) | <p>Gets the history of SIP status</p> |
| SipPlayWavFiles | [SipPlayWavFilesRequest](#ondewo.sip.SipPlayWavFilesRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Plays wav files during an ongoing call of an active SIP session</p> <p>Call scoping as for <code>SipTransferCall</code>: a present <code>x-ondewo-expected-call-id</code> metadatum must match <code>SipStatus.call_id</code>.</p>

Not idempotent (no idempotency_level): a repeat plays the files again. |
| SipMute | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | <p>Mutes the microphone in an ongoing call of an active SIP session</p> <p>Call scoping as for <code>SipTransferCall</code>. Sent by the in-container speech-to-speech pipeline it mutes only the bot's own mixer slot; sent by a remote client it sets the operator mute of <code>SipSetCallMediaControl</code>, which the pipeline cannot undo.</p>

Not idempotent (no idempotency_level): without a call it assigns NO_ONGOING_CALL and appends to the history. |
| SipUnMute | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | <p>Un-mutes the microphone in an ongoing call of an active SIP session</p> <p>Call scoping and the split between the pipeline's own mute and the operator mute as for <code>SipMute</code>.</p>

Not idempotent (no idempotency_level): without a call it assigns NO_ONGOING_CALL and appends to the history. |
| SipReportAnsweringMachineDetected | [SipReportAnsweringMachineDetectedRequest](#ondewo.sip.SipReportAnsweringMachineDetectedRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Reports that answering machine detection reached a verdict on the ongoing outgoing call. Sets the status <code>OUTGOING_CALL_ANSWERING_MACHINE_DETECTED</code> carrying <code>amd_result</code>; the call stays up.</p> <p>Called by the speech-to-speech pipeline (ONDEWO-CSI) inside the same container, i.e. over loopback only. Refused, and the current status left untouched, when no outgoing call is connected: the returned <code>SipStatus</code> then carries the refusal in <code>exception_name</code> and <code>description</code></p>

Not idempotent (no idempotency_level): assigns a status and records answering machine detection telemetry. |
| SipSetCallMediaControl | [SipSetCallMediaControlRequest](#ondewo.sip.SipSetCallMediaControlRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Call-scoped operator media control of the ongoing call: mute the bot and/or pause its listening.</p> <p>Metadata REQUIRED: <code>x-ondewo-expected-call-id</code> (must equal <code>SipStatus.call_id</code> of the ongoing call) and <code>x-ondewo-sip-call-control-token</code> (the per-container call-control token).</p> <p>Every request sets a desired level per owner and never toggles; a repeat leaves the level unchanged. The bot is muted while ANY owner holds a mute, and its listening is paused while ANY owner holds a pause.</p> <p>Returns the live status with <code>call_id</code>, <code>bot_muted</code>, <code>listening_paused</code> and <code>call_audio_streams</code> filled. Refusals are RETURNED in <code>exception_name</code> / <code>description</code> (<code>CallScopeMismatch</code>, <code>CallControlUnauthenticated</code>, <code>NoOngoingCall</code>, <code>AmdInProgress</code>, <code>CsiMediaControlFailed</code>) and never assigned to the shared status. When the pipeline refuses or fails, a requested pause is rolled back and a requested mute is kept (the safe direction); the returned fields carry the actual level.</p> <p>A request may carry a <code>warm_transfer_outcome</code> notice (participant owner only, refused otherwise with <code>exception_name=InvalidWarmTransferOutcomeNotice</code>). The notice is handed to the speech-to-speech pipeline whether or not the level changed, and the answer of the pipeline is returned in <code>SipStatus.warm_transfer_outcome_notice_status</code>.</p>

Deliberately unmarked although a repeat leaves the level unchanged: a retried attempt can land after a newer request of the same owner and restore a stale mute or pause. |
| SipStreamCallAudio | [SipCallAudioRequest](#ondewo.sip.SipCallAudioRequest) stream | [SipCallAudioResponse](#ondewo.sip.SipCallAudioResponse) stream | <p>Bidirectional live audio of the ongoing call.</p> <p>The first request MUST be <code>config</code> and must arrive within 2 seconds. Metadata as for <code>SipSetCallMediaControl</code>.</p> <p>LISTEN receives the caller (plus any conference participants) mixed with the bot. TALK sends the agent's audio to the caller; it REQUIRES <code>take_over</code>, i.e. the bot is muted and does not listen while the stream is connected, and in TALK the agent hears the caller only. Audio is LINEAR16 little-endian mono in 20 ms frames.</p> <p>gRPC status codes: <code>UNAUTHENTICATED</code> (token), <code>FAILED_PRECONDITION</code> (call id mismatch, no connected call, answering machine detection in progress, bot still speaking at TALK start), <code>INVALID_ARGUMENT</code> (missing or invalid <code>config</code>, wrong frame size), <code>RESOURCE_EXHAUSTED</code> (stream cap reached, a second TALK). A normal end sends one <code>ended</code> message and then OK.</p>

Not idempotent (no idempotency_level): a stream takes a slot and, in TALK, takes over the call. |
| SipSendDtmf | [SipSendDtmfRequest](#ondewo.sip.SipSendDtmfRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Send DTMF keys into the ongoing connected call, as RFC 4733 telephone-events (e.g. to navigate an IVR the bot called, or for an operator).</p> <p>Metadata as for <code>SipSetCallMediaControl</code>: <code>x-ondewo-expected-call-id</code> must equal <code>SipStatus.call_id</code> of the ongoing call; a peer outside the container presents <code>x-ondewo-sip-call-control-token</code> when the container has one.</p> <p>Returns the live status. Refusals are RETURNED in <code>exception_name</code> / <code>description</code> (<code>CallScopeMismatch</code>, <code>CallControlUnauthenticated</code>, <code>NoOngoingCall</code>, <code>AmdInProgress</code>, <code>InvalidDtmf</code>) and never assigned to the shared status. The keys are never logged in clear.</p>

Not idempotent (no idempotency_level): a retried attempt sends the keys again. |

 <!-- end services -->



## Scalar Value Types

| .proto Type | Notes | C++ | Java | Python | Go | C# | PHP | Ruby |
| ----------- | ----- | --- | ---- | ------ | -- | -- | --- | ---- |
| <a name="double" /> double |  | double | double | float | float64 | double | float | Float |
| <a name="float" /> float |  | float | float | float | float32 | float | float | Float |
| <a name="int32" /> int32 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint32 instead. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="int64" /> int64 | Uses variable-length encoding. Inefficient for encoding negative numbers – if your field is likely to have negative values, use sint64 instead. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="uint32" /> uint32 | Uses variable-length encoding. | uint32 | int | int/long | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="uint64" /> uint64 | Uses variable-length encoding. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum or Fixnum (as required) |
| <a name="sint32" /> sint32 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int32s. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sint64" /> sint64 | Uses variable-length encoding. Signed int value. These more efficiently encode negative numbers than regular int64s. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="fixed32" /> fixed32 | Always four bytes. More efficient than uint32 if values are often greater than 2^28. | uint32 | int | int | uint32 | uint | integer | Bignum or Fixnum (as required) |
| <a name="fixed64" /> fixed64 | Always eight bytes. More efficient than uint64 if values are often greater than 2^56. | uint64 | long | int/long | uint64 | ulong | integer/string | Bignum |
| <a name="sfixed32" /> sfixed32 | Always four bytes. | int32 | int | int | int32 | int | integer | Bignum or Fixnum (as required) |
| <a name="sfixed64" /> sfixed64 | Always eight bytes. | int64 | long | int/long | int64 | long | integer/string | Bignum |
| <a name="bool" /> bool |  | bool | boolean | boolean | bool | bool | boolean | TrueClass/FalseClass |
| <a name="string" /> string | A string must always contain UTF-8 encoded or 7-bit ASCII text. | string | String | str/unicode | string | string | string | String (UTF-8) |
| <a name="bytes" /> bytes | May contain any arbitrary sequence of bytes. | string | ByteString | str | []byte | ByteString | string | String (ASCII-8BIT) |
