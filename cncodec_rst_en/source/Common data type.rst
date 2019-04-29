.. _topics-Common data type:

Common data type
=============================

This part introduces the CNCodec common data type.

CN_HANDLE_VDEC
-----------------------

Decoder handle, 64-bit unsigned integer.

CN_HANDLE_VENC
------------------------

Encoder handle, 64-bit unsigned integer.

CN_VIDEO_CODEC_TYPE_E
-------------------------

The data format of decoder input and encoder output.

+----------------------+-------------+------------------------------+
| parameter name       | description | Remarks                      |
+======================+=============+==============================+
| CN_VIDEL_CODEC_MPEG4 | MPEG4       | decoding                     |
+----------------------+-------------+------------------------------+
| CN_VIDEL_CODEC_H264  | H264        | encoding, decoding           |
+----------------------+-------------+------------------------------+
| CN_VIDEL_CODEC_HEVC  | HEVC        | decoding                     |
+----------------------+-------------+------------------------------+
| CN_VIDEL_CODEC_JPEG  | JPEG        | encoding, decoding           |
+----------------------+-------------+------------------------------+
| CN_VIDEO_CODEC_MJPEG | MJPEG       | encoding (not supported yet) |
+----------------------+-------------+------------------------------+

CN_VIDEO_MODE_E
--------------------------

Sending mode of code stream.

+----------------------+-----------------+
| parameter name       | description     |
+======================+=================+
| CN_VIDEO_MODE_FRAME  | send by frame   |
+----------------------+-----------------+
| CN_VIDEO_MODE_STREAM | send by stream  |
+----------------------+-----------------+

CN_PIXEL_FORMAT_E
--------------------------

The pixel format of decoder output and encoder input.

+--------------------------+-------------------+------------------------------+
| parameter name           | description       | Remarks                      |
+==========================+===================+==============================+
| CN_PIXEL_FORMAT_YUV420SP | YUV420 SemiPlanar | encoding, decoding           |
+--------------------------+-------------------+------------------------------+
| CN_PIXEL_FORMAT_RGB24    | RGB24             | encoding, decoding           |
+--------------------------+-------------------+------------------------------+
| CN_PIXEL_FORMAT_BGR24    | BGR24             | encoding, decoding           |
+--------------------------+-------------------+------------------------------+

CN_VIDEO_DIE_MODE_E
--------------------------

De-interlace mode.

+-------------------------+------------------------------+
| parameter name          | description                  |
+=========================+==============================+
| CN_VIDEO_DIE_MODE_NODIE | force not to do De-interlace |
+-------------------------+------------------------------+
| CN_VIDEO_DIE_MODE_AUTO  | adaptive to do De-interlace  |
+-------------------------+------------------------------+
| CN_VIDEO_DIE_MODE_DIE   | force to do De-interlace     |
+-------------------------+------------------------------+

CN_VIDEO_IMAGE_INFO_S
--------------------------

Information of output image.

+------------------------+-------------------------------------------+
| parameter name         | description                               |
+========================+===========================================+
| enPixelFormat          | pixel format                              |
+------------------------+-------------------------------------------+
| u32FrameSize           | frame size                                |
+------------------------+-------------------------------------------+
| u32Height              | image height                              |
+------------------------+-------------------------------------------+
| u32Width               | image width                               |
+------------------------+-------------------------------------------+
| u64Pts                 | PTS(not supported yet)                    |
+------------------------+-------------------------------------------+
| u32Stride              | channel *Stride*                          |
+------------------------+-------------------------------------------+
| u64PhyAddr             | image physical address                    |
+------------------------+-------------------------------------------+
| u64VirAddr             | image virtual address                     |
+------------------------+-------------------------------------------+
| u64FrameIndex          | decode frame index                        |
+------------------------+-------------------------------------------+
| u64VideoIndex          | display frame index (not supported yet)   |
+------------------------+-------------------------------------------+
| u32BufIndex            | MLU cache index where the current frame is| 
|                        | located                                   |
+------------------------+-------------------------------------------+
| u64TransferUs          | transmission delay of the current frame   |
|                        | decoded image from codec to MLU (ms)      |
+------------------------+-------------------------------------------+
| u64DecodeDelayUs       | codec internal decoding  delay of the     |
|                        | current frame(ms)                         |
+------------------------+-------------------------------------------+
| u64SendCallbackDelayUs | delay in the current frame sent from      |
|                        | *CN_MPI_VDEC_Send* to the callback (ms)   |
+------------------------+-------------------------------------------+
| u64InputUs             | transmission delay of the current frame   | 
|                        | compressed data from host to device (ms)  |
+------------------------+-------------------------------------------+

CN_RECT_S
--------------------------

Position coordinates.

+-----------------+----------------------------------------------+
| parameter name  | description                                  |
+=================+==============================================+
| u32X            | absolute coordinate X, 2 pixel alignment     |
+-----------------+----------------------------------------------+
| u32Y            | absolute coordinate Y, 2 pixel alignment     |
+-----------------+----------------------------------------------+
| u32Width        | absolute coordinate width, 4 pixel alignment |
+-----------------+----------------------------------------------+
| u32Height       | absolute coordinate height, 4 pixel alignment|
+-----------------+----------------------------------------------+

CN_RECT_COORDINATE_E
--------------------------

Coordinate mode.

In the relative coordinate mode, the value of the member of CN_RECT_S is in the range of [0, 1000], and each unit represents 1/1000 of the image width or height.

+------------------------+-------------------------------------------+
| parameter name         | description                               |
+========================+===========================================+
| CN_RECT_RATIO_COOR     | relative coordinates (percentage)         |
+------------------------+-------------------------------------------+
| CN_RECT_ABS_COOR       | absolute coordinates                      |
+------------------------+-------------------------------------------+

CN_VIDEO_CROP_ATTR_S
--------------------------

Image cropping

+------------------------+-------------------------------------------+
| parameter name         | description                               |
+========================+===========================================+
| bEnable                | whether to enable image cropping          |
+------------------------+-------------------------------------------+
| enCropCoordinate       | the coordinate mode of the crop area      |
+------------------------+-------------------------------------------+
| stCropRect             | the coordinate of the crop area           |
+------------------------+-------------------------------------------+

CN_VIDEO_FRAME_RATE_S
--------------------------

Frame rate control, CNCodec has an active frame-dropping mechanism inside. When the input frame rate is too high and exceeds the decoding capability, the application can realize frame loss by frame rate control. The frame rate control parameter is used to set the active frame dropping mechanism.

Actively drop frames when *s32SrcFrmRate* > *s32DstFrmRate*:
    Frame-dropping rate = 1 - (s32SrcFrmRate / s32DstFrmRate)

when *s32SrcFrmRate == s32DstFrmRate*, does not actively drop frames

+------------------------+-------------------------------------------+
| parameter name         | description                               |
+========================+===========================================+
| bEnable                | whether cropping image enable             |
+------------------------+-------------------------------------------+
| s32SrcFrmRate          | frame rate of input                       |
+------------------------+-------------------------------------------+
| s32DstFrmRate          | frame rate of output                      |
+------------------------+-------------------------------------------+

CN_VIDEO_PP_ATTR_S
--------------------------

Image post-processing attribute.

+------------------------+----------------------------------------------------------------+
| parameter name         | description                                                    |
+========================+================================================================+
| stFrameRate            | frame rate control attribute                                   |
+------------------------+----------------------------------------------------------------+
| stCropAttr             | image cropping attribute                                       |
+------------------------+----------------------------------------------------------------+
| enDieMode              | de-interlace deinterlace mode                                  |
+------------------------+----------------------------------------------------------------+
| bIeEn                  | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| bDciEn                 | whether to enable dynamic contrast adjustment                  |
+------------------------+----------------------------------------------------------------+
| bNrEn                  | whether to enable noise reduction                              |
+------------------------+----------------------------------------------------------------+
| bHistEn                | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| bEsEn                  | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| bSpEn                  | whether to enable image sharpening                             |
+------------------------+----------------------------------------------------------------+
| u32Constrast           | dynamic contrast adjustment intensity, the default value is 32 |
+------------------------+----------------------------------------------------------------+
| u32DieStrength         | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| u32IeStrength          | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| u32SfStrength          | airspace denoising strength 0-2047, the default value is 128   |
+------------------------+----------------------------------------------------------------+
| u32TfStrength          | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| u32CfStrength          | color gamut denoising strength 0-255, the default value is 8   |
+------------------------+----------------------------------------------------------------+
| u32CTfStrength         | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| u32CvbsStrength        | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| u32DeMotionBlurring    | reserved, must be set to 0                                     |
+------------------------+----------------------------------------------------------------+
| u32SpStrength          | image sharpening intensity 0-100, the default value is 32      |
+------------------------+----------------------------------------------------------------+

CN_MLU_P2P_BUFFER_S
--------------------------

Information of output buffer for receiving output data.

+-----------------+-------------------------------------------+
| parameter name  | description                               |
+=================+===========================================+
| addr            | virtual address of output buffer memory   |
+-----------------+-------------------------------------------+
| len             | length of output buffer                   |
+-----------------+-------------------------------------------+

CN_BUFFER_TYPE_E
--------------------------

Type of output buffer.

+-----------------+---------------------+
| parameter name  | description         |
+=================+=====================+
| CN_MLU_BUFFER   | MLU buffer          |
+-----------------+---------------------+
| CN_CPU_BUFFER   | CPU buffer          |
+-----------------+---------------------+

CN_MLU_P2P_ATTR_S
--------------------------

Configuration information of output buffer.

+-----------------+---------------------------------------------------+
| parameter name  | description                                       |
+=================+===================================================+
| buffer_num      | number of output buffer                           |
+-----------------+---------------------------------------------------+
| buffer_type     | type of output buffer, MLU / CPU                  |
+-----------------+---------------------------------------------------+
| \*p_buffers     | pointer of information structure of output buffer |
+-----------------+---------------------------------------------------+

CN_VIDEO_CREATE_ATTR_S
--------------------------

Decoder creation attributes.

+--------------------------+---------------------------------------------------------+
| parameter name           | description                                             |
+==========================+=========================================================+
| u32VdecDeviceID          | device ID, 0-(device num-1), each device ID             |
|                          | points to a board                                        |
+--------------------------+---------------------------------------------------------+
| enInputVideoCodec        | decode input data format                                |
+--------------------------+---------------------------------------------------------+
| enVideoMode              | code stream transmission method                         |
+--------------------------+---------------------------------------------------------+
| u32MaxWidth              | maximum supported resolution (width)                    |
+--------------------------+---------------------------------------------------------+
| u32MaxHeight             | maximum supported resolution (height)                   |
+--------------------------+---------------------------------------------------------+
| u32TargetWidth           | output resolution (width), 2 pixel alignment            |
+--------------------------+---------------------------------------------------------+
| u32TargetHeight          | output resolution (height), 2 pixel alignment           |
+--------------------------+---------------------------------------------------------+
| u32TargetWidthSubstream  | substream output resolution (width) 2 pixel alignment,  |
|                          | 0 = off substream output                                |
+--------------------------+---------------------------------------------------------+
| u32TargetHeightSubstream | substream output resolution (height) 2 pixel alignment, |
|                          | 0 = off substream output                                |
+--------------------------+---------------------------------------------------------+
| u32MaxFrameSize          | maximum *ES frame* size (not supported yet)             |
+--------------------------+---------------------------------------------------------+
| u32EsBufCount            | number of ES stream buffers (not supported yet)         |
+--------------------------+---------------------------------------------------------+
| u32ImageBufCount         | image buffer format (not supported yet)                 |
+--------------------------+---------------------------------------------------------+
| enOutputPixelFormat      | output pixel format                                     |
+--------------------------+---------------------------------------------------------+
| enVideoCreateMode        | decoding mode (not supported yet)                       |
+--------------------------+---------------------------------------------------------+
| stPostProcessAttr        | image post-processing attribute                         |
+--------------------------+---------------------------------------------------------+
| u64UserData              | callback function user context                          |
+--------------------------+---------------------------------------------------------+
| pImageCallBack           | callback function pointer of decoded picture            |
+--------------------------+---------------------------------------------------------+
| mluP2pAttr               | configuration information of MLU cache in P2P mode      |
+--------------------------+---------------------------------------------------------+

CN_VIDEO_PIC_PARAM_S
--------------------------

Information of input data.

+------------------------+------------------------+
| parameter name         | description            |
+========================+========================+
| nBitStreamDataLen      | data length            |
+------------------------+------------------------+
| nBitStreamData         | data address           |
+------------------------+------------------------+
| u32Width               | width of image         |
+------------------------+------------------------+
| u32Height              | height of image        |
+------------------------+------------------------+

CN_VDEC_DEVICE_CAPABILITY_S
-------------------------------

Information of single device channel.

+------------------------+---------------------------------------------------------+
| parameter name         | description                                             |
+========================+=========================================================+
| u32DeviceID            | device ID                                               |
+------------------------+---------------------------------------------------------+
| u32MluIndex            | MLU index, used to provide device index to cnrt         |
|                        | interface when applying for MLU memory                  |
+------------------------+---------------------------------------------------------+
| u32FreeChannels        | number of free decoding channels                        |
+------------------------+---------------------------------------------------------+
| u32UsedChannels        | number of used decoding channels                        |
+------------------------+---------------------------------------------------------+

CN_VDEC_CAPABILITY_S
-------------------------------

Information of all devices.

+------------------+---------------------------------------------------+
| parameter name   | description                                       |
+==================+===================================================+
| u32VdecDeviceNum | number of devices                                 |
+------------------+---------------------------------------------------+
| VdecDeviceList[] | information of all devices                        |
+------------------+---------------------------------------------------+

CN_VDEC_IMAGE_CALLBACK
-------------------------------

Callback function of decoded image:

CN_VOID (\*CN_VDEC_IMAGE_CALLBACK)(CN_VIDEO_IMAGE_INFO_S \*pImageOutput, CN_U64 u64UserData);

+------------------+---------------------------------------------------+
| parameter name   | description                                       |
+==================+===================================================+
| pImageOutput     | information of output image                       |
+------------------+---------------------------------------------------+
| u64UserData      | user context                                      |
+------------------+---------------------------------------------------+

CN_LOG_LEVEL
-------------------------------

Log level, enumerated type.

+------------------------+------------------------+
| parameter name         | description            |
+========================+========================+
| CN_LOG_NONE            | none-level log         |
+------------------------+------------------------+
| CN_LOG_ERR             | error log              |
+------------------------+------------------------+
| CN_LOG_WARN            | warning log            |
+------------------------+------------------------+
| CN_LOG_INFO            | information log        |
+------------------------+------------------------+
| CN_LOG_DEBUG           | debug log              |
+------------------------+------------------------+

CN_LOG_CALLBACK
------------------------------

Callback function of log:

CN_VOID (\*CN_LOG_CALLBACK)(CN_LOG_LEVEL level, const char \*msg);

+------------------+---------------------------------+
| parameter name   | description                     |
+==================+=================================+
| level            | log level                       |
+------------------+---------------------------------+
| msg              | log information                 |
+------------------+---------------------------------+

CNResult
------------------------------

definition of  CNCodec interface return value.

+-----------------------------------+-------+--------------------------------------------+
| parameter name                    | value | description                                |
+===================================+=======+============================================+
| CN_SUCCESS                        | 0     | success                                    |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_INVALID_VALUE            | 1     | invalid parameter                          |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_OUT_OF_MEMORY            | 2     | out of storage                             |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_NOT_INITIALIZED          | 3     | not initialized                            |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_DEINITHALIZED            | 4     | has been destroyed                         |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_PROFILER_DISABLED        | 5     | profiler is disabled                       |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_PROFILER_NOT_INITIALIZED | 6     | profiler is not initialized                |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_ALREADY_STARTED          | 7     | already started                            |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_ALREADY_STOPPED          | 8     | already stopped                            |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_OS_CALL                  | 9     | failed to call OS system                   |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_INVALID_FORMAT           | 10    | unsupported encoding format                |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_NO_RESOURCE              | 11    | out of resources                           |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_NO_DEVICE                | 100   | device does not exist                      |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_INVALID_DEVICE           | 101   | invalid device                             |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_INVALID_IMAGE            | 200   | invalid image                              |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_INVALID_CONTEXT          | 201   | invalid context                            |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_INVALID_DATA             | 202   | invalid data                               |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_INVALID_SOURCE           | 300   | invalid input source                       |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_FILE_NOT_FOUND           | 301   | file dose not exist                        |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_INVALID_HANDLE           | 400   | invalid handle                             |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_NOT_FOUND                | 500   | not found                                  |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_NOT_READY                | 600   | not ready                                  |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_LAUNCH_FAILED            | 700   | failed to launch                           |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_LAUNCH_OUT_OF_RESOURCES  | 701   | memory allocation failed during launch     |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_LAUNCH_TIMEOUT           | 702   | launch time out                            |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_UNKNOWN                  | 999   | unknown error                              |
+-----------------------------------+-------+--------------------------------------------+
| CN_ERROR_SYSCALL                  | 1000  | failed to call SYS system                  |
+-----------------------------------+-------+--------------------------------------------+

CN_VENC_RC_t
------------------------------

Mode of encoder rate control.

+------------------+---------------------------------+
| parameter name   | description                     |
+==================+=================================+
| CBR              | fixed bit rate                  |
+------------------+---------------------------------+
| VBR              | variable bit rate               |
+------------------+---------------------------------+

CN_VENC_ATTR_H264_CBR_S
------------------------------

Encoder CBR rate control parameters.

+------------------+---------------------------------------------------+
| parameter name   | description                                       |
+==================+===================================================+
| u32Gop           | Gop value of H.264, range: [1, 65536]             |
+------------------+---------------------------------------------------+
| u32StatTime      | CBR code rate statistics time, unit: seconds,     |
|                  | range: [1, 60]                                    |
+------------------+---------------------------------------------------+
| u32SrcFrmRate    | VI input frame rate, the value is required to be  |
|                  | larger than *fr32DstFrmRate*                      |
+------------------+---------------------------------------------------+
| fr32DstFrmRate   | encoder output frame rate, unit: fps              |
+------------------+---------------------------------------------------+
| u32BitRate       | average bitrate, unit: kbps, range: [2, 102400]   |
+------------------+---------------------------------------------------+
| u32FluctuateLevel| the fluctuation level of the maximum code rate    |
|                  | relative to the average code rate, the range:     |
|                  | [0, 5], the recommended fluctuation level is 0.   |
+------------------+---------------------------------------------------+

CN_VENC_ATTR_H264_VBR_S
------------------------------

Encoder VBR rate control parameters.

+------------------+---------------------------------------------------+
| parameter name   | description                                       |
+==================+===================================================+
| u32Gop           | Gop value of H.264, range: [1, 65536]             |
+------------------+---------------------------------------------------+
| u32StatTime      | VBR code rate statistics time, unit: seconds,     |
|                  | range: [1, 60]                                    |
+------------------+---------------------------------------------------+
| u32SrcFrmRate    | VI input frame rate, the value is required to be  |
|                  | larger than *fr32DstFrmRate*                      |
+------------------+---------------------------------------------------+
| fr32DstFrmRate   | encoder output frame rate, unit: fps              |
+------------------+---------------------------------------------------+
| u32MaxBitRate    | maximum bitrate, unit: kbps, range: [2, 102400]   |
+------------------+---------------------------------------------------+
| u32MaxQp         | maximum image QP the encoder supports,            |
|                  | [u32MinQp, 51]                                    |
+------------------+---------------------------------------------------+
| u32MinQp         | minimum image QP the encoder supports, [0, 51]    |
+------------------+---------------------------------------------------+

CN_VENC_CREATE_ATTR_S
------------------------------

Attributes of encoder channel.

+--------------------------+---------------------------------------------------------+
| parameter name           | description                                             |
+==========================+=========================================================+
| u32VencDeviceID          | device ID, 0-(device num-1), each device ID             |
|                          | points to a board                                        |
+--------------------------+---------------------------------------------------------+
| VideoCodecType           | encoding data format, support MJPEG, H264, JPEG         |
+--------------------------+---------------------------------------------------------+
| rate_control_mode        | code rate control mode                                  |
+--------------------------+---------------------------------------------------------+
| u32MaxWidth              | maximum supported width of image to be encoded          |
+--------------------------+---------------------------------------------------------+
| u32MaxHeight             | maximum supported height of image to be encoded         |
+--------------------------+---------------------------------------------------------+
| pixel_format             | format of input pixel                                   |
+--------------------------+---------------------------------------------------------+
|                          | output resolution, 2 pixel alignment                    |
| u32TargetWidth           |                                                         |
|                          | when the output resolution is larger than 0, input      | 
|                          | images smaller than this resolution will be discarded,  | 
+--------------------------+ and input images larger than or equal to this resolution|
|                          | will be resized to output resolution and then be encoded|
|                          | for output                                              |
| u32TargetHeight          |                                                         |
|                          | when the output resolution is 0, output according to the| 
|                          | original resolution of the input data.                  |
+--------------------------+---------------------------------------------------------+
| H264CBR                  | CBR rate control parameter                              |
+--------------------------+---------------------------------------------------------+
| H264VBR                  | VBR rate control parameter                              |
+--------------------------+---------------------------------------------------------+
| bcolor2gray              | grayscale encoding settings (color image converted to   |
|                          | grayscale image and then encoded)                       |
+--------------------------+---------------------------------------------------------+
| encode_crop              | crop encoding settings                                  |
+--------------------------+---------------------------------------------------------+
| mluP2pAttr               | configuration information of MLU cache in P2P mode      |
+--------------------------+---------------------------------------------------------+
| pEncodeCallBack          | callback function pointer of encoded picture            |
+--------------------------+---------------------------------------------------------+
| pu64UserData             | user context of callback function                       |
+--------------------------+---------------------------------------------------------+

CN_VENC_DEVICE_CAPABILITY_S
------------------------------

Information of single encoding channel.

+------------------------+---------------------------------------------------------+
| parameter name         | description                                             |
+========================+=========================================================+
| u32DeviceID            | device ID                                               |
+------------------------+---------------------------------------------------------+
| u32MluIndex            | MLU index, used to provide device index to cnrt         |
|                        | interface when applying for MLU memory                  |
+------------------------+---------------------------------------------------------+
| u32FreeChannels        | number of free encoding channels                        |
+------------------------+---------------------------------------------------------+
| u32UsedChannels        | number of used encoding channels                        |
+------------------------+---------------------------------------------------------+

CN_VENC_CAPABILITY_S
------------------------------

Information of all encoding devices.

+------------------+---------------------------------------------------+
| parameter name   | description                                       |
+==================+===================================================+
| u32VencDeviceNum | number of devices                                 |
+------------------+---------------------------------------------------+
| VencDeviceList[] | information of all devices                        |
+------------------+---------------------------------------------------+