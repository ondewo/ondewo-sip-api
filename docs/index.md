# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [ondewo/sip/sip.proto](#ondewo/sip/sip.proto)
    - [SipEndCallRequest](#ondewo.sip.SipEndCallRequest)
    - [SipPlayWavFilesRequest](#ondewo.sip.SipPlayWavFilesRequest)
    - [SipRegisterAccountRequest](#ondewo.sip.SipRegisterAccountRequest)
    - [SipStartCallRequest](#ondewo.sip.SipStartCallRequest)
    - [SipStartCallRequest.HeadersEntry](#ondewo.sip.SipStartCallRequest.HeadersEntry)
    - [SipStartSessionRequest](#ondewo.sip.SipStartSessionRequest)
    - [SipStatus](#ondewo.sip.SipStatus)
    - [SipStatus.HeadersEntry](#ondewo.sip.SipStatus.HeadersEntry)
    - [SipStatusHistoryResponse](#ondewo.sip.SipStatusHistoryResponse)
    - [SipTransferCallRequest](#ondewo.sip.SipTransferCallRequest)
    - [SipTransferCallRequest.HeadersEntry](#ondewo.sip.SipTransferCallRequest.HeadersEntry)
  
    - [SipStatus.StatusType](#ondewo.sip.SipStatus.StatusType)
  
    - [Sip](#ondewo.sip.Sip)
  
- [Scalar Value Types](#scalar-value-types)



<a name="ondewo/sip/sip.proto"></a>
<p align="right"><a href="#top">Top</a></p>

## ondewo/sip/sip.proto



<a name="ondewo.sip.SipEndCallRequest"></a>

### SipEndCallRequest
<p>Ends an ongoing call of the active SIP session of the active SIP account</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hard_hangup | [bool](#bool) |  | Set to <code>True</code> to forcefully hang up the call |






<a name="ondewo.sip.SipPlayWavFilesRequest"></a>

### SipPlayWavFilesRequest
<p>Plays a list of wav files</p>


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| wav_files | [bytes](#bytes) | repeated | Wav files as bytes in a list that will be played |






<a name="ondewo.sip.SipRegisterAccountRequest"></a>

### SipRegisterAccountRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  | Account name of the sip user. Usually something like <code>sip-user-1@mydomain.com</code> or <code>sip-user-1@192.168.123.123</code> which uses the default SIP port <code>5060</code>. Also a non-default SIP port can be specified via <code>sip-user-1@mydomain.com:5099</code> to connect to a SIP server running on port <code>5099</code> |
| password | [string](#string) |  | Password of the account |
| auth_username | [string](#string) |  | Optional: authentication user name |
| outbound_proxy | [string](#string) |  | Optional: outbound proxy address, e.g. <code>my.outbound.proxy.com</code> |






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
| auto_answer_interval | [int32](#int32) |  | answer interval |






<a name="ondewo.sip.SipStatus"></a>

### SipStatus



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
| headers | [SipTransferCallRequest.HeadersEntry](#ondewo.sip.SipTransferCallRequest.HeadersEntry) | repeated | The headers to include when transferring the call |






<a name="ondewo.sip.SipTransferCallRequest.HeadersEntry"></a>

### SipTransferCallRequest.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |





 <!-- end messages -->


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


 <!-- end enums -->

 <!-- end HasExtensions -->


<a name="ondewo.sip.Sip"></a>

### Sip
<p>ONDEWO-SIP API available at <a href="https://github.com/ondewo/ondewo-sip-api">GitHub</a></p>

<p>SIP LifeCycle is explained at <a href="https://thanhloi2603.wordpress.com/2017/06/10/sip-lifecycle-overview/">here</a></p>

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| SipStartSession | [SipStartSessionRequest](#ondewo.sip.SipStartSessionRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Starts a new SIP session for an account registered at a SIP server. <code>RegisterAccount</code> need to be called before.</p> |
| SipEndSession | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | <p>Ends a SIP session for an account registered at a SIP server</p> |
| SipStartCall | [SipStartCallRequest](#ondewo.sip.SipStartCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Starts a call in an active SIP session for an account registered at a SIP server</p> |
| SipEndCall | [SipEndCallRequest](#ondewo.sip.SipEndCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Ends a call in an active SIP session for an account registered at a SIP server</p> |
| SipTransferCall | [SipTransferCallRequest](#ondewo.sip.SipTransferCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Transfers a call in an active SIP session for an account registered at a SIP server to another SIP account or phone number specified by <code>transfer_id</code></p> |
| SipRegisterAccount | [SipRegisterAccountRequest](#ondewo.sip.SipRegisterAccountRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Registers s SIP account at a SIP server</p> |
| SipGetSipStatus | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | <p>Gets the current SIP status</p> |
| SipGetSipStatusHistory | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatusHistoryResponse](#ondewo.sip.SipStatusHistoryResponse) | <p>Gets the history of SIP status</p> |
| SipPlayWavFiles | [SipPlayWavFilesRequest](#ondewo.sip.SipPlayWavFilesRequest) | [SipStatus](#ondewo.sip.SipStatus) | <p>Plays wav files during an ongoing call of an active SIP session</p> |
| SipMute | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | <p>Mutes the microphone in an ongoing call of an active SIP session</p> |
| SipUnMute | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | <p>Un-mutes the microphone in an ongoing call of an active SIP session</p> |

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
