# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [ondewo/sip/sip.proto](#ondewo/sip/sip.proto)
    - [EndCallRequest](#ondewo.sip.EndCallRequest)
    - [PlayWavFilesRequest](#ondewo.sip.PlayWavFilesRequest)
    - [RegisterAccountRequest](#ondewo.sip.RegisterAccountRequest)
    - [SipMicrophoneResponse](#ondewo.sip.SipMicrophoneResponse)
    - [SipStatus](#ondewo.sip.SipStatus)
    - [SipStatus.HeadersEntry](#ondewo.sip.SipStatus.HeadersEntry)
    - [SipStatusHistoryResponse](#ondewo.sip.SipStatusHistoryResponse)
    - [StartCallRequest](#ondewo.sip.StartCallRequest)
    - [StartCallRequest.HeadersEntry](#ondewo.sip.StartCallRequest.HeadersEntry)
    - [StartSessionRequest](#ondewo.sip.StartSessionRequest)
    - [TransferCallRequest](#ondewo.sip.TransferCallRequest)
    - [TransferCallRequest.HeadersEntry](#ondewo.sip.TransferCallRequest.HeadersEntry)
  
    - [SipMicrophoneResponse.SipMicrophoneType](#ondewo.sip.SipMicrophoneResponse.SipMicrophoneType)
    - [SipStatus.StatusType](#ondewo.sip.SipStatus.StatusType)
  
    - [Sip](#ondewo.sip.Sip)
  
- [Scalar Value Types](#scalar-value-types)



<a name="ondewo/sip/sip.proto"></a>
<p align="right"><a href="#top">Top</a></p>

## ondewo/sip/sip.proto



<a name="ondewo.sip.EndCallRequest"></a>

### EndCallRequest
Ends an ongoing call of the active SIP session of the active SIP account


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hard_hangup | [bool](#bool) |  | Set to <code>True</code> to forcefully hang up the call |






<a name="ondewo.sip.PlayWavFilesRequest"></a>

### PlayWavFilesRequest
Plays a list of wav files


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| wav_files | [bytes](#bytes) | repeated | Wav files as bytes in a list that will be played |






<a name="ondewo.sip.RegisterAccountRequest"></a>

### RegisterAccountRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  | Account name of the sip user. Usually something like <code>sip-user-1@mydomain.com</code> or <code>sip-user-1@192.168.123.123</code> which uses the default SIP port <code>5060</code>. Also a non-default SIP port can be specified via <code>sip-user-1@mydomain.com:5099</code> to connect to a SIP server running on port <code>5099</code> |
| password | [string](#string) |  | Password of the account |
| auth_username | [string](#string) |  | Optional: authentication user name |
| outbound_proxy | [string](#string) |  | Optional: outbound proxy address, e.g. <code>myoutboundproxy.com</code> |






<a name="ondewo.sip.SipMicrophoneResponse"></a>

### SipMicrophoneResponse
Microphone respone


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  | Account name of the sip user. Usually something like <code>sip-user-1@mydomain.com</code> or <code>sip-user-1@192.168.123.123</code> which uses the default SIP port <code>5060</code>. Also a non-default SIP port can be specified via <code>sip-user-1@mydomain.com:5099</code> to connect to a SIP server running on port <code>5099</code> |
| timestamp | [google.protobuf.Timestamp](#google.protobuf.Timestamp) |  | Timestamp of the status |






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






<a name="ondewo.sip.SipStatus.HeadersEntry"></a>

### SipStatus.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="ondewo.sip.SipStatusHistoryResponse"></a>

### SipStatusHistoryResponse
History of SIP status


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| status_history | [SipStatus](#ondewo.sip.SipStatus) | repeated | History of SIP status |






<a name="ondewo.sip.StartCallRequest"></a>

### StartCallRequest
Request to start the call with the active SIP session of the active SIP account


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| callee_id | [string](#string) |  | SIP account name |
| headers | [StartCallRequest.HeadersEntry](#ondewo.sip.StartCallRequest.HeadersEntry) | repeated | Headers to include when starting the call |






<a name="ondewo.sip.StartCallRequest.HeadersEntry"></a>

### StartCallRequest.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="ondewo.sip.StartSessionRequest"></a>

### StartSessionRequest
Request for starting a new SIP session for a specified account


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  | Account name of the sip user. Usually something like <code>sip-user-1@mydomain.com</code> or <code>sip-user-1@192.168.123.123</code> which uses the default SIP port <code>5060</code>. Also a non-default SIP port can be specified via <code>sip-user-1@mydomain.com:5099</code> to connect to a SIP server running on port <code>5099</code> |
| auto_answer_interval | [int32](#int32) |  | answer interval |






<a name="ondewo.sip.TransferCallRequest"></a>

### TransferCallRequest
Request for tranfering a call with or without headers


| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| transfer_id | [string](#string) |  | The account name or phone number to transfer the call to |
| headers | [TransferCallRequest.HeadersEntry](#ondewo.sip.TransferCallRequest.HeadersEntry) | repeated | The headers to include when transfering the call |






<a name="ondewo.sip.TransferCallRequest.HeadersEntry"></a>

### TransferCallRequest.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |





 <!-- end messages -->


<a name="ondewo.sip.SipMicrophoneResponse.SipMicrophoneType"></a>

### SipMicrophoneResponse.SipMicrophoneType
Microphone status

| Name | Number | Description |
| ---- | ------ | ----------- |
| SIP_MICROPHONE_MUTED | 0 | Microphone is muted |
| SIP_MICROPHONE_UNMUTED | 1 | Microphone is unmuted |
| SIP_MICROPHONE_WAV_FILES_PLAYED | 2 | Microphone has played wav files |



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
| INCOMING_CALL_CONNECTED | 6 | SIP account incoming call is conneted |
| TRANSFER_CALL_INITIATED | 7 | SIP account starts transfering the call |
| SOFT_HANGUP_INITIATED | 8 | SIP account hangs up the ongoing call |
| HARD_HANGUP_INITIATED | 9 | SIP account forcefully hangs up by terminating the SIP program |
| INCOMING_CALL_FAILED | 10 | SIP account cannot accept the incoming call |
| OUTGOING_CALL_FAILED | 11 | SIP account cannot do an outbound call |
| INCOMING_CALL_FINISHED | 12 | SIP account finished the ongoing incoming call |
| OUTGOING_CALL_FINISHED | 13 | SIP account finished the ongoing outgoing call |
| SESSION_REGISTRATION_FAILED | 14 | Registration of SIP account to SIP server failed |
| SESSION_STARTED | 15 | SIP account started a new SIP session via a SIP server |
| SESSION_ENDED | 16 | SIP account ended active sip session with SIP server |


 <!-- end enums -->

 <!-- end HasExtensions -->


<a name="ondewo.sip.Sip"></a>

### Sip
ONDEWO-SIP API available at <a href="https://github.com/ondewo/ondewo-sip-api>">GitHub</a>

SIP LifeCyle is explained at <a href="https://thanhloi2603.wordpress.com/2017/06/10/sip-lifecycle-overview/">here</a>

| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| StartSession | [StartSessionRequest](#ondewo.sip.StartSessionRequest) | [SipStatus](#ondewo.sip.SipStatus) | Starts a new SIP session for an account registered at a SIP server. <code>RegisterAccount</code> need to be called before. |
| EndSession | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | Ends a SIP session for an account registered at a SIP server |
| StartCall | [StartCallRequest](#ondewo.sip.StartCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | Starts a call in an active SIP session for an account registered at a SIP server |
| EndCall | [EndCallRequest](#ondewo.sip.EndCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | Ends a call in an active SIP session for an account registered at a SIP server |
| TransferCall | [TransferCallRequest](#ondewo.sip.TransferCallRequest) | [SipStatus](#ondewo.sip.SipStatus) | Transfers a call in an active SIP session for an account registered at a SIP server to another SIP account or phone number specified by <code>tranfer_id</code> |
| RegisterAccount | [RegisterAccountRequest](#ondewo.sip.RegisterAccountRequest) | [SipStatus](#ondewo.sip.SipStatus) | Registers s SIP account at a SIP server |
| GetSipStatus | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) | Gets the current SIP status |
| GetSipStatusHistory | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatusHistoryResponse](#ondewo.sip.SipStatusHistoryResponse) | Gets the history of SIP status |
| PlayWavFiles | [PlayWavFilesRequest](#ondewo.sip.PlayWavFilesRequest) | [SipMicrophoneResponse](#ondewo.sip.SipMicrophoneResponse) | Plays wav files during an ongoing call of an active SIP session |
| Mute | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipMicrophoneResponse](#ondewo.sip.SipMicrophoneResponse) | Mutes the microphone in an ongoing call of an active SIP session |
| UnMute | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipMicrophoneResponse](#ondewo.sip.SipMicrophoneResponse) | Unmutes the microphone in an ongoing call of an active SIP session |

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
