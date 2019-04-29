.. _topics-APIs:

APIs
=============================

This part introduces the CNCodec APIs.

CN_MPI_SoftwareVersion
---------------------------------

::

    API: const char * CN_MPI_SoftwareVersion();
    Brief: get the SDK lib version number
    Param: none
    Return: string of version number, x.x.x

CN_MPI_Init
---------------------------------

::

    API: CNResult CN_MPI_Init();
    Brief: SDK initialization, this interface must be called before calling other CNCodec interfaces
    Param: none
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_Exit
---------------------------------

::

    API: CNResult CN_MPI_Exit();
    Brief: destruct the SDK and release the resource CN_MPI_INIT
    Param: none
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_VDEC_GetCapability
---------------------------------

::

    API: CNResult CN_MPI_VDEC_GetCapability(CN_VDEC_CAPABILITY_S *pstCapalility);
    Brief: get the decoder status of all devices
    Param pstCapalility: pointer of decoder status.
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_VDEC_Create
---------------------------------

::

    API: CNResult CN_MPI_VDEC_Create(CN_HANDLE_VDEC *phDecoder, CN_VIDEO_CREATE_ATTR_S *pstCreateAttr);
    Brief: create a decoder channel
    Param phDecoder: pointer of decoder handle
    Param pstCreateAttr: pointer of decoder attributes
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_VDEC_Destroy
---------------------------------

::

    API: CNResult CN_MPI_VDEC_Destroy(CN_HANDLE_VDEC hDecoder);
    Brief: destroy the decoder channel
    Param hDecoder: decoder handle
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_VDEC_Send
---------------------------------

::

    API: CNResult CN_MPI_VDEC_Send(CN_HANDLE_VDEC hDecoder, CN_VIDEO_PIC_PARAM_S *pstPicParams);
    Brief: send data to the decoder channel
    Param phDecoder: decoder handle
    Param pstPicParams: information of data to be sent, pointer
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_MLU_P2P_ReleaseBuffer
---------------------------------

::

    API: CNResult CN_MPI_MLU_P2P_ReleaseBuffer(CN_HANDLE_VDEC hDecoder, int buffer_index);
    Brief: release buffer
    Param hDecoder: decoder handle
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_SetLogCallback
---------------------------------

::

    API: CN_VOID CN_MPI_SetLogCallback(CN_LOG_CALLBACK callback);
    Brief: set the global log callback function. If it is not set, or is NULL, the log is output to stderr.
    Param callback: callback function of log
    Return: void

CN_MPI_SetFatalCallback
---------------------------------

::

    API: CN_VOID CN_MPI_SetFatalCallback(CN_FATAL_CALLBACK callback);
    Brief: set the global callback function for fatal error. If it is not set, or is NULL, the log is output to stderr.
    Param callback: callback function of Fatal
    Return: void

CN_MPI_VENC_GetCapability
---------------------------------

::

    API: CNResult CN_MPI_VENC_GetCapability(CN_VENC_CAPABILITY_S *pstCapalility);
    Brief: get the encoder status of all devices
    Param pstCapalility: pointer of encoder status
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_VENC_Create
---------------------------------

::

    API: CNResult CN_MPI_VENC_Create(CN_HANDLE_VDEC *phEncoder, CN_VENC_CREATE_ATTR_S *pstCreateAttr);
    Brief: create encoder channel
    Param phEncoder: pointer of encoder handle
    Param pstCreateAttr: pointer of encoder attributes
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_VENC_Destroy
---------------------------------

::

    API: CNResult CN_MPI_VENC_Destroy(CN_HANDLE_VDEC hEncoder);
    Brief: destroy the encoder channel
    Param hEncoder: encoder handle
    Return: returns 0 on success and non-zero on failure, its value is CNResult

CN_MPI_VENC_Send
--------------------------------

::

    API: CNResult CN_MPI_VENC_Send(CN_HANDLE_VDEC hEncoder, CN_VIDEO_PIC_PARAM_S *pstPicParams);
    Brief: send data to the encoder channel
    Param hEncoder: encoder handle
    Param pstPicParams: information of data to be sent, pointer
    Return: returns 0 on success and non-zero on failure, its value is CNResult