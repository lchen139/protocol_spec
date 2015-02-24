# SmartDeviceLink Protocol

## 2. Frame Headers
### 2.1 Version 1 Frame Header
<table>
  <tr>
    <th colspan="3" width="25%">Byte 1</th>
    <th width="25%">Byte 2</th>
    <th width="25%">Byte 3</th>
    <th width="25%">Byte 4</th>
  </tr>
  <tr>
    <td width="12.5%">Version</td>
    <td width="3.125%">C</td>
    <td width="9.375%">Frame Type</td>
    <td>Service Type</td>
    <td>Control Frame Info</td>
    <td>Session ID</td>
  </tr>
</table>

<table>
  <tr>
    <th width="250">Byte 5</th>
    <th width="25%">Byte 6</th>
    <th width="25%">Byte 7</th>
    <th width="25%">Byte 8</th>
  </tr>
  <tr>
    <td colspan="4" align="center">Data Size</td>
  </tr>
</table>

### 2.2 Version 2 Frame Header

<table>
  <tr>
    <th colspan="3" width="25%">Byte 1</th>
    <th colspan="1"width="25%">Byte 2</th>
    <th width="25%">Byte 3</th>
    <th width="25%">Byte 4</th>
  </tr>
  <tr>
    <td width="12.5%">Version</td>
    <td width="3.125%">E</td>
    <td width="9.375%">Frame Type</td>
    <td>Service Type</td>
    <td>Control Frame Info</td>
    <td>Session ID</td>
  </tr>
</table>

<table >
  <tr>
    <th width="300">Byte 5</th>
    <th width="25%">Byte 6</th>
    <th width="25%">Byte 7</th>
    <th width="25%">Byte 8</th>
  </tr>
  <tr>
    <td colspan="4" align="center">Data Size</td>
  </tr>
</table>

<table>
  <tr>
    <th width="300">Byte 9</th>
    <th width="25%">Byte 10</th>
    <th width="25%">Byte 11</th>
    <th width="25%">Byte 12</th>
  </tr>
  <tr>
    <td colspan="4" align="center">Message ID</td>
  </tr>
</table>

### 2.3 Frame Header Fields
<table width="100%">
  <tr>
    <th>Field</th>
    <th>Size</th>
    <th width="75%">Description</th>
  </tr>
  <tr>
    <td>Version</td>
    <td>4 bit</td>
    <td>Protocol Version Number</td>
  </tr>
  <tr>
    <td>C</td>
    <td>1 bit</td>
    <td><b>Compression Flag</b> <br> 0x0 This packet is not compressed <br> 0x1 This packet is compressed <br> <b>Note:</b> Only available in Protocol Version 1</td>
  </tr>
  <tr>
    <td>E</td>
    <td>1 bit</td>
    <td><b>Encryption Flag</b> <br> 0x0 This packet is not encrypted <br> 0x1 This packet is encrypted <br> <b>Note:</b> Only available in Protocol Version 2</td>
  </tr>
  <tr>
    <td>Frame Type</td>
    <td>3 bit</td>
    <td>
      0x00 Control Frame <br>
      0x01 Single Frame <br>
      0x02 First Frame <br>
      0x03 Consecutive Frame <br>
      0x04 - 0x07 Reserved
    </td>
  </tr>
  <tr>
    <td>Service Type</td>
    <td>8 bit</td>
    <td>
      0x00 Control Service<br>
      0x01 - 0x06 Reserved<br>
      0x07 Remote Procedure Call (RPC) Service<br>
      0x08 - 0x09 Reserved<br>
      0x0A PCM Service<br>
      0x0B Video Service<br>
      0x0C - 0x0E Reserved<br>
      0x0F Bulk Data (Hybrid Service)<br>
      0x10 - 0xFF Reserved
    </td>
  </tr>
  <tr>
    <td>Frame Info</td>
    <td>8 bit</td>
    <td>
      <b>Frame Type = 0x00 (Control Frame)</b><br>
      0x00 Heartbeat<br>
      0x01 Start Service<br>
      0x02 Start Service ACK<br>
      0x03 Start Service NACK<br>
      0x04 End Service<br>
      0x05 End Service ACK<br>
      0x06 End Service NACK<br>
      0x07 - 0xFD Reserved<br>
      0xFE Service Data ACK<br>
      0xFF Heartbeat ACK<br>
      <b>Frame Type = 0x01 (Single Frame)</b><br>
      0x00 Reserved // TODO: needs clarification<br>
      <b>Frame Type = 0x02 (First Frame)</b><br>
      0x00 Reserved // TODO: needs clarification<br>
      <b>Frame Type = 0x03 (Consecutive Frame)</b><br>
      0x00 Last Frame<br>
      0x01 - 0xFF Frame Number
    </td>
  </tr>
  <tr>
    <td>Session ID</td>
    <td>8 bit</td>
    <td>The session identifier</td>
  </tr>
  <tr>
    <td>Data Size</td>
    <td>32 bit</td>
    <td>
      <b>Frame Type = 0x00 (Control Frame)</b><br>
      0x00 Reserved // TODO: this was copied over but the specification is not clear. What about 0x01-0xFFFFFFFF?<br>
      <b>Frame Type = 0x02 (First Frame)</b><br>
      0x08 The data size for a first frame is always 8 bytes. In the payload, the first four bytes denote the Total Size of the data contained in all consecutive frames, and the second four bytes denotes the number of consecutive frames following this one<br>
      <b>Frame Type = 0x01 or 0x03 (Single or Consecutive Frame)</b><br>
      The total bytes in this frame
    </td>
  </tr>
  <tr>
    <td>Message ID</td>
    <td>32 bit</td>
    <td>The message identifier, used to uniquely identify this message</td>
  </tr>
</table>

## 3. Establishing Communication

### 3.1 Transport Layer

### 3.2 Version Negotiation

#### 3.2.1 Success

#### 3.2.2 Failure

## 4. Services

### 4.1 Starting a Service

#### 4.1.1 Success

#### 4.1.2 Failure

### 4.2 Ending a Service

### 4.3 RPC Service

### 4.4 Hybrid Service

### 4.5 Control Service

### 4.6 Audio Service

### 4.7 H.264 Service

### 4.8 Reserved Services

## 5 Ending Communication
