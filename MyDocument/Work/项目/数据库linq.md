SELECT * FROM `Param`;
SELECT * FROM `ModIndex`;
SELECT * FROM `PresentImportDev`;
SELECT * FROM `DevList` WHERE `devname` ='TD48A';
SELECT * FROM `FunctionConfiguration` WHERE `function_code` ='PEQB';

TD48A 
SELECT * FROM `Param` WHERE `proid` ='67175681';
SELECT * FROM `Param` WHERE `proid` ='67175682';
SELECT * FROM `Param` WHERE `proid` ='67175683';
SELECT * FROM `ModIndex` WHERE `proid` ='67175681';
SELECT * FROM `ModIndex` WHERE `proid` ='67175682' and enable ='T';
SELECT * FROM `ModIndex` WHERE `proid` ='67175683';
SELECT * FROM ChannelLink WHERE `proid` ='67175681';
SELECT * FROM ChannelLink WHERE `proid` ='67175681'  GROUP BY  paramname ;
SELECT * FROM ControlTypeAndParam WHERE `proid` ='67175681';
FunctionConfiguration
TD48A AMP
67175686 67175685 67175684
SELECT * FROM `Param` WHERE `proid` ='67175684';
SELECT * FROM `Param` WHERE `proid` ='67175685';
SELECT * FROM `Param` WHERE `proid` ='67175686';
SELECT * FROM `Param` WHERE `module` ='PresentInfo';
SELECT * FROM `ModIndex` WHERE `proid` ='67175684';
SELECT * FROM `FunctionConfiguration` WHERE `device_code` ='67175683';
SELECT * FROM ChannelLink WHERE `proid` ='67175684';
SELECT * FROM ChannelFunction WHERE `proid` ='67175684';
SELECT * FROM GPIOTypeAndParam WHERE `proid` ='67175684';
SELECT * FROM ControlTypeAndParam WHERE `proid` ='67175684';
SELECT * FROM DevCFun WHERE DevIDList LIKE '%67175686%';
UPDATE DevCFun set DevIDList='67175684,'||DevIDList WHERE DevIDList LIKE '%67175686%';

ChannelFunction
SELECT * FROM `ChannelFunction` WHERE `proid` ='67175683';
总表
SELECT * FROM DevList;

DA2044AD
17826050
Out0-Out1
SELECT * FROM `Param` WHERE `proid` ='17826050';
SELECT * FROM `ChannelFunction` WHERE `proid` ='17826050';
SELECT * FROM `FunctionConfiguration` WHERE `device_code` ='17826050';
SELECT * FROM `Param` WHERE `parmname` ='ChanTypeCount';
SELECT * FROM `ModIndex` WHERE `proid` ='17826050';
SELECT * FROM DevCFun dc WHERE DevIDList LIKE '%17826050%';
17826050,临时改成51
SELECT * FROM DevCFun dc WHERE DevIDList LIKE '%17826050%';
SELECT * FROM DevCFun dc WHERE DevIDDescription  LIKE '%功放%';
2025-06-19
GPA4KD:16777750   GPA4K:16777749
SELECT * FROM `Param` WHERE `proid` ='16777749';
SELECT * FROM `ChannelFunction` WHERE `proid` ='16777749';
SELECT * FROM `FunctionConfiguration` WHERE `device_code` ='16777749';
SELECT * FROM `ModIndex` WHERE `proid` ='16777749';
SELECT * FROM `DevCFun` WHERE DevIDList LIKE '%17826050%';
SELECT * FROM ChannelLink  cf  WHERE `proid` ='16777749';
SELECT * FROM ControlTypeAndParam WHERE `proid` ='16777750';
SELECT * FROM ControlTypeAndParam WHERE `proid` ='16777749';

UPDATE DevCFun set DevIDList='16777749,'||DevIDList WHERE DevIDList LIKE '%16777750%';
2025 08 12
16777752 GpA4KD奥雷   
SELECT * FROM `Param` WHERE `proid` ='16777752';
SELECT * FROM `ChannelFunction` WHERE `proid` ='16777752';
SELECT * FROM `FunctionConfiguration` WHERE `device_code` ='16777752';
SELECT * FROM `ModIndex` WHERE `proid` ='16777752';
SELECT * FROM `DevCFun` WHERE `proid` ='16777750';

SELECT * FROM ChannelLink  cf  WHERE `proid` ='16777752';
SELECT * FROM ControlTypeAndParam WHERE `proid` ='16777752';
SELECT * FROM DevCFun WHERE DevIDList LIKE '%16777750%';

UPDATE DevCFun set DevIDList='16777752,'||DevIDList WHERE DevIDList LIKE '%16777750%';


、、POE80 ID=33686660 33686662 33686666  POE80AE  33686670
单通道 ID=33686668   POE80AB  33686671
SELECT * FROM `ModIndex` WHERE `proid` ='33686671';
SELECT * FROM `Param` WHERE `proid` ='33686671';
SELECT * FROM FunctionConfiguration fc  WHERE device_code   ='33686671';
SELECT * FROM `GPIOTypeAndParam` WHERE `proid` ='33686671';
SELECT * FROM ChannelFunction cf  WHERE `proid` ='33686671';
SELECT * FROM ChannelLink  cf  WHERE `proid` ='33686671';
SELECT * FROM ControlTypeAndParam cf  WHERE `proid` ='33686671';
SELECT * FROM DevCFun  WHERE `DevIDList` LIKE  '%33686671%';
字符串拼接
UPDATE DevCFun set DevIDList='33686671,'||DevIDList WHERE DevIDList LIKE '%33686668%';
POE80  33686662   33686666
SELECT * FROM `Param` WHERE `proid` ='33686671';
SELECT * FROM `ModIndex` WHERE `proid` ='33686666';
SELECT * FROM ChannelFunction cf  WHERE `proid` ='33686662';
SELECT * FROM FunctionConfiguration fc  WHERE device_code   ='33686662';
SELECT * FROM DevCFun  WHERE `DevIDList` LIKE  '%33686666%';
UPDATE DevCFun set DevIDList='33686668,'||DevIDList WHERE DevIDList LIKE '%33686666%';
POE80AE 33686670 POE80BE 33686671

33686665 33686659 PAT71

SELECT * FROM `Param` WHERE `proid` ='33686659';

0408U 67305729
SELECT * FROM `Param` WHERE `proid` ='67305729';
SELECT * FROM `Param` WHERE `module` ='ChanAMP';
SELECT * FROM `ModIndex` WHERE `proid` ='67305729';
SELECT * FROM `FunctionConfiguration` WHERE `device_code` ='67305729';
SELECT * FROM ChannelLink WHERE `proid` ='67175686';
SELECT * FROM ChannelFunction WHERE `proid` ='67175686';
SELECT * FROM GPIOTypeAndParam WHERE `proid` ='67305729';
SELECT * FROM ControlTypeAndParam WHERE `proid` ='67175686';
SELECT * FROM DevCFun  WHERE `DevIDList` LIKE  '%67175686%';
UPDATE DevCFun set DevIDList='67305729,'||DevIDList WHERE DevIDList LIKE '%67175686%';
SELECT * FROM DevCFun WHERE DevIDList LIKE '%67305729%';


