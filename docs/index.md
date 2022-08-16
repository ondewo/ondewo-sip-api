# Protocol Documentation
<a name="top"></a>

## Table of Contents

- [ondewo/sip/sip.proto](#ondewo/sip/sip.proto)
    - [EndCallRequest](#ondewo.sip.EndCallRequest)
    - [PlayWavFilesRequest](#ondewo.sip.PlayWavFilesRequest)
    - [RegisterAccountRequest](#ondewo.sip.RegisterAccountRequest)
    - [SipStatus](#ondewo.sip.SipStatus)
    - [SipStatus.HeadersEntry](#ondewo.sip.SipStatus.HeadersEntry)
    - [SipStatusHistoryResponse](#ondewo.sip.SipStatusHistoryResponse)
    - [StartCallRequest](#ondewo.sip.StartCallRequest)
    - [StartCallRequest.HeadersEntry](#ondewo.sip.StartCallRequest.HeadersEntry)
    - [StartSessionRequest](#ondewo.sip.StartSessionRequest)
    - [TransferCallRequest](#ondewo.sip.TransferCallRequest)
    - [TransferCallRequest.HeadersEntry](#ondewo.sip.TransferCallRequest.HeadersEntry)
  
    - [SipStatus.StatusType](#ondewo.sip.SipStatus.StatusType)
  
    - [Sip](#ondewo.sip.Sip)
  
- [Scalar Value Types](#scalar-value-types)



<a name="ondewo/sip/sip.proto"></a>
<p align="right"><a href="#top">Top</a></p>

## ondewo/sip/sip.proto



<a name="ondewo.sip.EndCallRequest"></a>

### EndCallRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| hard_hangup | [bool](#bool) |  |  |






<a name="ondewo.sip.PlayWavFilesRequest"></a>

### PlayWavFilesRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| wav_files | [bytes](#bytes) | repeated |  |






<a name="ondewo.sip.RegisterAccountRequest"></a>

### RegisterAccountRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  |  |
| password | [string](#string) |  |  |






<a name="ondewo.sip.SipStatus"></a>

### SipStatus



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  |  |
| timestamp | [google.protobuf.Timestamp](#google.protobuf.Timestamp) |  |  |
| status_type | [SipStatus.StatusType](#ondewo.sip.SipStatus.StatusType) |  |  |
| callee_id | [string](#string) |  |  |
| transfer_call_id | [string](#string) |  |  |
| headers | [SipStatus.HeadersEntry](#ondewo.sip.SipStatus.HeadersEntry) | repeated |  |






<a name="ondewo.sip.SipStatus.HeadersEntry"></a>

### SipStatus.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="ondewo.sip.SipStatusHistoryResponse"></a>

### SipStatusHistoryResponse



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| status_history | [SipStatus](#ondewo.sip.SipStatus) | repeated |  |






<a name="ondewo.sip.StartCallRequest"></a>

### StartCallRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| callee_id | [string](#string) |  |  |
| headers | [StartCallRequest.HeadersEntry](#ondewo.sip.StartCallRequest.HeadersEntry) | repeated |  |






<a name="ondewo.sip.StartCallRequest.HeadersEntry"></a>

### StartCallRequest.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |






<a name="ondewo.sip.StartSessionRequest"></a>

### StartSessionRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| account_name | [string](#string) |  |  |
| auto_answer_interval | [int32](#int32) |  |  |






<a name="ondewo.sip.TransferCallRequest"></a>

### TransferCallRequest



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| transfer_id | [string](#string) |  |  |
| headers | [TransferCallRequest.HeadersEntry](#ondewo.sip.TransferCallRequest.HeadersEntry) | repeated |  |






<a name="ondewo.sip.TransferCallRequest.HeadersEntry"></a>

### TransferCallRequest.HeadersEntry



| Field | Type | Label | Description |
| ----- | ---- | ----- | ----------- |
| key | [string](#string) |  |  |
| value | [string](#string) |  |  |





 <!-- end messages -->


<a name="ondewo.sip.SipStatus.StatusType"></a>

### SipStatus.StatusType


| Name | Number | Description |
| ---- | ------ | ----------- |
| no_session | 0 |  |
| registered | 1 |  |
| ready | 2 |  |
| incoming_call_initiated | 3 |  |
| outgoing_call_initiated | 4 |  |
| outgoing_call_connected | 5 |  |
| incoming_call_connected | 6 |  |
| transfer_call_initiated | 7 |  |
| soft_hangup_initiated | 8 |  |
| hard_hangup_initiated | 9 |  |
| incoming_call_failed | 10 |  |
| outgoing_call_failed | 11 |  |
| incoming_call_finished | 12 |  |
| outgoing_call_finished | 13 |  |


 <!-- end enums -->

 <!-- end HasExtensions -->


<a name="ondewo.sip.Sip"></a>

### Sip


| Method Name | Request Type | Response Type | Description |
| ----------- | ------------ | ------------- | ------------|
| StartSession | [StartSessionRequest](#ondewo.sip.StartSessionRequest) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |
| EndSession | [.google.protobuf.Empty](#google.protobuf.Empty) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |
| StartCall | [StartCallRequest](#ondewo.sip.StartCallRequest) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |
| EndCall | [EndCallRequest](#ondewo.sip.EndCallRequest) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |
| TransferCall | [TransferCallRequest](#ondewo.sip.TransferCallRequest) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |
| RegisterAccount | [RegisterAccountRequest](#ondewo.sip.RegisterAccountRequest) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |
| GetSipStatus | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatus](#ondewo.sip.SipStatus) |  |
| GetSipStatusHistory | [.google.protobuf.Empty](#google.protobuf.Empty) | [SipStatusHistoryResponse](#ondewo.sip.SipStatusHistoryResponse) |  |
| PlayWavFiles | [PlayWavFilesRequest](#ondewo.sip.PlayWavFilesRequest) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |
| Mute | [.google.protobuf.Empty](#google.protobuf.Empty) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |
| UnMute | [.google.protobuf.Empty](#google.protobuf.Empty) | [.google.protobuf.Empty](#google.protobuf.Empty) |  |

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
