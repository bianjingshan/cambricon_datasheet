.. _topics-APIs:

APIs
=============================

本章介绍CNCodec接口。

CN_MPI_SoftwareVersion
---------------------------------

::

    API: const char * CN_MPI_SoftwareVersion();
    描述: 获取SDK lib版本号
    参数: 无
    返回值: 版本号字符串，x.x.x

CN_MPI_Init
---------------------------------

::

    API: CNResult CN_MPI_Init();
    描述: SDK初始化，调用CNCodec其他接口前必须调用该接口
    参数: 无
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_Exit
---------------------------------

::

    API: CNResult CN_MPI_Exit();
    描述: 析构SDK，释放资源CN_MPI_INIT
    参数: 无
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_VDEC_GetCapability
---------------------------------

::

    API: CNResult CN_MPI_VDEC_GetCapability(CN_VDEC_CAPABILITY_S *pstCapalility);
    描述: 获取所有device的解码器状态
    参数: 
        pstCapalility：解码器状态结构体指针
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_VDEC_Create
---------------------------------

::

    API: CNResult CN_MPI_VDEC_Create(CN_HANDLE_VDEC *phDecoder, CN_VIDEO_CREATE_ATTR_S *pstCreateAttr);
    描述: 创建解码器通道
    参数: 
        phDecoder: 解码器句柄指针
        pstCreateAttr: 解码器属性
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_VDEC_Destroy
---------------------------------

::

    API: CNResult CN_MPI_VDEC_Destroy(CN_HANDLE_VDEC hDecoder);
    描述: 销毁解码器通道
    参数: 
        phDecoder: 解码器句柄指针
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_VDEC_Send
---------------------------------

::

    API: CNResult CN_MPI_VDEC_Send(CN_HANDLE_VDEC hDecoder, CN_VIDEO_PIC_PARAM_S *pstPicParams);
    描述: 向解码器通道发送数据
    参数: 
        phDecoder: 解码器句柄指针
        pstPicParams: 发送数据信息
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_MLU_P2P_ReleaseBuffer
---------------------------------

::

    API: CNResult CN_MPI_MLU_P2P_ReleaseBuffer(CN_HANDLE_VDEC hDecoder, int buffer_index);
    描述: 释放输出内存，释放后解码器或编码器可重用此内存
    参数: 
        phDecoder: 解码器或编码器句柄指针
        buffer_index: 缓存index
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_SetLogCallback
---------------------------------

::

    API: CN_VOID CN_MPI_SetLogCallback(CN_LOG_CALLBACK callback);
    描述: 设置全局日志回调函数，如果不设置，或者是为NULL，则日志输出终端
    参数: 
        callback: 日志回调函数
    返回值: void

CN_MPI_VENC_GetCapability
---------------------------------

::

    API: CNResult CN_MPI_VENC_GetCapability(CN_VENC_CAPABILITY_S *pstCapalility);
    描述: 获取所有device的编码器状态
    参数: 
        pstCapalility：编码器状态结构体指针
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_VENC_Create
---------------------------------

::

    API: CNResult CN_MPI_VENC_Create(CN_HANDLE_VDEC *phEncoder, CN_VENC_CREATE_ATTR_S *pstCreateAttr);
    描述: 创建编码器通道
    参数: 
        phEncoder：编码器句柄指针
        pstCreateAttr：编码器属性
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_VENC_Destroy
---------------------------------

::

    API: CNResult CN_MPI_VENC_Destroy(CN_HANDLE_VDEC hEncoder);
    描述: 销毁编码器通道
    参数: 
        hEncoder：编码器句柄指针
    返回值: 0=成功；非0=失败，其值为CNResult

CN_MPI_VENC_Send
--------------------------------

::

    API: CNResult CN_MPI_VENC_Send(CN_HANDLE_VDEC hEncoder, CN_VIDEO_PIC_PARAM_S *pstPicParams);
    描述: 向编码器通道发送数据
    参数: 
        hEncoder：编码器句柄指针
        pstPicParams：发送数据信息
    返回值: 0=成功；非0=失败，其值为CNResult