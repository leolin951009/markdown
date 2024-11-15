## InsApp_Movie_VideoSplit
1. 判断是否为I帧
2. s_mov_ctrl.loop_num是什么？
3. 查询是否需要先删除文件，如果需要则先删除文件，（判断条件为1.行车文件是否达到设置的循环空间 2.sd剩余空间是否在？G以上）
4. dcf是文件管理系统
5. 创建新文件的文件名
6. InsApp_Stream_MuxStart是用来干什么的？
7. 启动split任务，FileSplitTaskEntry
   1. InsApp_Record_DashCamDeleteFile，判断是否需要删除文件，需要则执行删除。



查询行车状态 InsApp_Record_DashCamStatusCheck

## 目前行车逻辑
1. 录像侵占（行车文件size+sd free size）剩11.6G以下时，就报卡满，需要删除录像文件，取消卡满状态。
2. 录像侵占到sd free size 4G以下，报卡满，且此时 （行车文件size+sd free size）> 11.6G，删除行车文件至sd free size > 4G，也能取消卡满状态。
3. 录像侵占（行车文件size+sd free size）大于11.6G时，执行循环空间调整。
4. 正常的行车录像，总会保留4G以上的sd free size。

## 关于split线程阻塞导致存文件异常的问题，split线程优先级抬高
1. 码流处理线程优先级 s_StreamCtrl[StreamIdx].task.priority = (0==StreamIdx)?10:18;
2. split线程优先级 SplitPriority = (InsApp_Movie_GetRealRecordTime(pVideoInfo->StreamId)>=INS_MOVIE_RECORD_25_MINUTES_LIMIT)?120:100;
