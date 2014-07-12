image-rename
============

image-rename 是一个用来对 JPG/RAW/TIF 图像和其它文件进行重命名的命令行工具。

features and tips for image-rename
image-rename 功能和使用技巧

coding: utf-8

version: 
版本: 
1.5, 2014-03-30

License: GPL V3 or BSD License
许可证: GPL 第3版，或者 BSD 许可证

Homepage: 
主页：
https://sourceforge.net/projects/emacslocale/files/image-rename/

Test for:
测试环境:
* Ubuntu 10.04 i386;
* GNU bash, version 4.1.5;
* GNU sed version 4.2.1
 
Description: image-rename is a command line tool to rename JPG/RAW/TIF
 image and other files, by modifing special suffix, prefix and date. it
 also can remove EXIF metadata for JPG/RAW/TIF images, and some other
 useful features:
   * probe JPG/RAW image files for camera bands;
   * remove EXIF metadata for JPG/RAW images, and save to new files;
   * rename filename by modify suffix;
   * rename filename by add prefix with date and special text;

说明：
   image-rename 是一个用来对 JPG/RAW/TIF 图像
   和其它文件进行重命名的命令行工具。它通过修改指定的扩展名，前缀文字和
   日期来实现。还可以用来清除 JPG/RAW/TIF 图像的EXIF 
   元数据，以及一些其它的实用功能：
   * 检测 JPG/RAW 图像文件的相机品牌；
   * 移除 JPG/RAW 图像的 EXIF 元数据, 并另存为新的文件；
   * 通过修改扩展名的方式，对文件进行重命名；
   * 通过添加日期和指定的文字前缀，对文件进行重命名；

 ---------------------------------------------

目录
第一部分：image-rename 功能示例
  * 1 (已完成) 查看 image-rename 程序的使用说明
  * 2 (已完成) 根据数码相机/摄像机图像文件名格式，推测相机/摄像机品牌
  * 3 (已完成) 按图像文件的创建日期（通常即拍照日期），在文件名前面加上日期
  * 4 (已完成) 清除文件名前面的日期文字（即恢复“例301”中的原始文件名）
  * 5 (已完成) 检测图像文件名是否为*.JPG或*.JPEG格式。

  * 6 (已完成) 在文件名前面加上指定的文字
  * 7 (已完成) 在文件名前面加上指定的文字和日期
  * 8 (已完成) 把数码相机图像中的文件名头部改名

第二部分：image-rename 使用技巧
  * 例1(已完成): 查看照片是用什么品牌相机拍的
  * 例2(已完成): 改变某些扩展名（如THM）的图像文件名为新的
  扩展名JPG，方便在手机/平板电脑上查看，或
  者上传到网络相册和QQ空间

  * 例3(已完成): 把例2中的THM图像扩展名改回原始文件名
  * 例4(已完成): 在文件名前面自动添加文件的修改日期
 
  * 例5(已完成): 在文件名前面自动添加指定文字

  * 例6(已完成): 清除文件名中包含的日期（如发现相机的拍照日期设置错误）

  * 例7(已完成): 去掉已添加的文件名前面的文字
  * 例8(已完成): 改变/替换文件名前面的文字，改为其它相机的文件名编号规则

  * 例9(已完成): 去除JPG图像中的EXIF元数据，而不是只改变文件名

附录1：使用 imagemagick 软件包 的 convert 命令清除JPG图像的EXIF元数据

附录2: 使用 exiftool 命令清除JPG图像的EXIF元数据

 =============================================

第一部分：功能示例

* 1 (已完成) 查看 image-rename 程序的使用说明
  image-rename --readme

* 2 (已完成) 根据数码相机/摄像机图像文件名格式，推测相机/摄像机品牌
  用法：image-rename -b 文件/多个文件
       image-rename -b
  说明：
    如果未给出文件名，则根据当前语言环境（简体中文或其
    它），列出各品牌数码相机图像的文件名格式说明（目前只
    支持简体中文和英文帮助信息）。

    ** -b 参数代表相机/摄像机的品牌（band）；
    ** 支持包含路径的文件名；
    ** 能正确识别包含空格的文件名；
    ** 支持包含通配符的多个文件名；

  例201：检测指定目录下的所有图像文件拍照使用的相机品牌
  命令：image-rename -b ~/DCIM/*/*
  应用场景：
  技术说明：先用file命令检测是否为JPG图像文件，再分析文件名格式，
     判断相机品牌。
         如果文件名是xxx.JPG格式，但实际上文件并不是一个真正
     的JPG图像文件，程序会自动忽略该文件。
输出示例：
-----------------
1 * 忽略: '/home/user/DCIM/101GEDSC/DIR'	(忽略目录, 只支持文件操作)
2 * '/home/user/DCIM/101GEDSC/GEDC0001.JPG'	(相机: GE; 格式: JPG)
3 * '/home/user/DCIM/101GEDSC/GEDC0001.THM'	(相机: GE; 格式: JPG)
4 * '/home/user/DCIM/101GEDSC/GEDC0002.JPG'	(相机: GE; 格式: JPG)
5 * '/home/user/DCIM/101GEDSC/image-rename.jpg'	(相机: 未知; 格式: JPG)
6 * '/home/user/DCIM/101GEDSC/IMG_20140214_201314.jpg'	(相机: 不确定; 格式: JPG)
7 * '/home/user/DCIM/101GEDSC/README.txt'	(未知的文件格式，或者文件不可用)
8 * '/home/user/DCIM/101GEDSC/test.tar.gz'	(格式: GZ)
-----------------


* 3 (已完成) 按图像文件的创建日期（通常即拍照日期），在文件名前面加上日期
  用法：image-rename -d 文件/多个文件
  说明：-d参数代表date(日期)

  例301：将指定目录下的所有文件的文件名更改为“年年年年-月月-日日_原文件名”格式
  命令：image-rename -d ~/DCIM/*/*
  输出示例：
-----------------
在文件名前面添加日期（自动检测图像/文件的拍照或修改日期，格式为“年年年年-月月-日日_”）...

1 * 忽略: '/home/user/DCIM/101GEDSC/DIR'	(忽略目录, 只支持文件操作)
2 * 重命名: '/home/user/DCIM/101GEDSC/GEDC0001.JPG' -> '2014-03-23_GEDC0001.JPG' 	[ OK ]
3 * 重命名: '/home/user/DCIM/101GEDSC/GEDC0001.THM' -> '2014-03-23_GEDC0001.THM' 	[ OK ]
4 * 重命名: '/home/user/DCIM/101GEDSC/GEDC0002.JPG' -> '2014-03-23_GEDC0002.JPG' 	[ OK ]
5 * 重命名: '/home/user/DCIM/101GEDSC/image-rename.jpg' -> '2014-03-23_image-rename.jpg' 	[ OK ]
6 * 重命名: '/home/user/DCIM/101GEDSC/IMG_20140214_201314.jpg' -> '2014-03-23_IMG_20140214_201314.jpg' 	[ OK ]
7 * 重命名: '/home/user/DCIM/101GEDSC/README.txt' -> '2014-03-23_README.txt' 	[ OK ]
8 * 重命名: '/home/user/DCIM/101GEDSC/test.tar.gz' -> '2014-03-23_test.tar.gz' 	[ OK ]

-----------------

  应用场景：保险公司业务员/交警/公检法办案取证，政府部门办证拍照，
     地理勘探测绘，旅行者/摄影爱好者按日期整理照片，提高工作
     效率，方便查找
  免责声明：本程序非商业软件，未进行严格的测试，请勿在重要的商业
     计算机上使用本软件。
         可能出现的风险：更名时可能出现文件重名，导致某些文件
     被覆盖或更改----作者不对此承担任何直接或间接损失。
  技术说明：
    ** 本程序不是按JPG图像的EXIF信息来提取拍照日期；
    ** 如果拍照时相机日期未正确设置，或者后来有旋转图像操作，
       或者用图像软件（如PhotoShop等)处理过文件，或者清除/
       修改过EXIF元数据，可能出现改名后的日期不准确。

-----------------
* 4 (已完成) 清除文件名前面的日期文字（即恢复“例301”中的原始文件名）

  用法：image-rename -rd 文件/多个文件
  说明：-rd参数代表remove date（删除日期）
  举例：image-rename -rd ~/DCIM/*/*
  应用场景：
  技术说明： 
  输出示例：
-----------------
移除文件名前面的日期文字（“年年年年-月月-日日_”格式）...
1 * 重命名: '/home/user/DCIM/101GEDSC/2014-03-23_GEDC0001.JPG' -> 'GEDC0001.JPG' 	[ OK ]
2 * 重命名: '/home/user/DCIM/101GEDSC/2014-03-23_GEDC0001.THM' -> 'GEDC0001.THM' 	[ OK ]
3 * 重命名: '/home/user/DCIM/101GEDSC/2014-03-23_GEDC0002.JPG' -> 'GEDC0002.JPG' 	[ OK ]
4 * 重命名: '/home/user/DCIM/101GEDSC/2014-03-23_image-rename.jpg' -> 'image-rename.jpg' 	[ OK ]
5 * 重命名: '/home/user/DCIM/101GEDSC/2014-03-23_IMG_20140214_201314.jpg' -> 'IMG_20140214_201314.jpg' 	[ OK ]
6 * 重命名: '/home/user/DCIM/101GEDSC/2014-03-23_README.txt' -> 'README.txt' 	[ OK ]
7 * 重命名: '/home/user/DCIM/101GEDSC/2014-03-23_test.tar.gz' -> 'test.tar.gz' 	[ OK ]

8 * 忽略: '/home/user/DCIM/101GEDSC/DIR'	(忽略目录, 只支持文件操作)
-----------------


* 5 (已完成) 检测图像文件名是否为*.JPG或*.JPEG格式。
  如果不是，自动在文件名后面添加.JPG后缀；
  如果已经是*.JPG或者*.JPEG，忽略该文件不做任何更改

  用法：image-rename -j 文件/多个文件
  说明：* -j参数代表自动更名为JPG文件名后缀

  例401：image-rename -j ~/DCIM/*/*
     对指定目录下的所有JPG图像文件自动添加JPG扩展名。如果已经带有 JPG 扩展名，
     忽略该文件，不执行任何改名操作。

  应用场景：某些数码相机拍照时会自动保存大图（原始照片）和小图（缩略
     图），如通用（GE）相机，会同时生成两个文件GEDC0001.JPG
    （大图）和GEDC0001.THM（缩略图）。可以使用本选项自动把
     *.THM小图改名为*.THM.JPG，方便上传到网络相册或QQ空间，或
    者在手机/平板电脑上查看小图像。
  技术说明：文件名可以带路径参数 

  输出示例：
-----------------
更改文件的扩展名为 'JPG' ...
1 * 忽略: '/home/user/DCIM/101GEDSC/DIR'	(忽略目录, 只支持文件操作)
2 * 忽略: '/home/user/DCIM/101GEDSC/GEDC0001.JPG'
3 * 重命名: '/home/user/DCIM/101GEDSC/GEDC0001.THM' -> 'GEDC0001.THM.JPG' 	[ OK ] 
4 * 忽略: '/home/user/DCIM/101GEDSC/GEDC0002.JPG'
5 * 忽略: '/home/user/DCIM/101GEDSC/image-rename.jpg'
6 * 忽略: '/home/user/DCIM/101GEDSC/IMG_20140214_201314.jpg'
7 * 跳过: '/home/user/DCIM/101GEDSC/README.txt'	(文件实际格式不符合扩展名'JPG')
8 * 跳过: '/home/user/DCIM/101GEDSC/test.tar.gz'	(不会对压缩文件进行操作)
-----------------

* 6 (已完成) 在文件名前面加上指定的文字
  用法：image-rename -p 前缀文字 文件/多个文件
  说明：-p 参数代表 prefix(前缀文字)

  例601：将当前目录下的所有扩展名为JPG的图像文件的文件名更改为“上海文件名.JPG”格式
  命令：image-rename -p 上海 *.JPG
  应用场景：保险公司业务员/交警/公检法办案取证，政府部门办证拍照，地理勘探测绘，
     旅行者/摄影爱好者对照片进行批量改名，提高工作效率，也方便查找和复制转移
  免责声明：本程序非商业软件，未进行严格测试，请勿在重要场合或商业计算机上使用本软件。
         可能出现的风险：更名时可能出现文件重名，导致某些文件
     被覆盖或其它可能出现的异常，作者不承担因此导致的任何直接或
   间接责任。

-----------------
* 7 (已完成) 在文件名前面加上指定的文字和日期
  用法：image-rename -pd 前綴文字 文件/多个文件 
  说明：等同于第4项和第6项中功能的合并。 
  应用场景：
  技术说明： 

-----------------
* 8 (已完成) 把数码相机图像中的文件名头部改名
  用法：image-rename -rmp 前缀文字 文件/多个文件
  用法：image-rename -rpp 原前缀 新前缀 文件/多个文件

  说明：-rmp 参数代表 REMOVE prefix(移除前缀)
  说明：-rpp 参数代表 REPLACE prefix(替换前缀)
  已知缺陷：

  应用场景：
     避免他人直接从图像文件名看出拍照使用的相机品牌，保护个人
     和公司秘密。
  技术说明：
     ** 本程序仅修改文件名，不会修改或清除JPG图像中的EXIF信息。
        其他人仍可以从图像的EXIF信息中，查看相机拍照的相关信息。
        如果有需要，请选用其它图像处理软件来清除图像中EXIF信息。


 =============================================
第二部分：image-rename 使用技巧

例如，数码相机内存卡里有2个文件，分别是
/home/user/DCIM/101GEDSC/GEDC0001.JPG
/home/user/DCIM/101GEDSC/GEDC0001.THM

* 例1(已完成):查看照片是用什么品牌相机拍的
 参数：-b 文件名

 具体操作：
 先进入图像目录：
 cd /home/user/DCIM/101GEDSC/

 然后运行：
  image-rename -b *

 输出信息示例：
----------------
根据JPG/RAW/TIFF图像文件名格式, 推测相机/摄像机品牌...
1 * test.JPG/GEDC0360.THM	(相机: GE; 格式: JPG)
2 * test.JPG/GEDC0360.JPG	(相机: GE; 格式: JPG)
----------------

输出信息解释：
    上面的信息显示相机品牌为GE（美国通用），两个文件实际都是JPG格式。
通过查看文件大小，可以确定JPG结尾的文件是大图像，THM结尾的是缩略图。

技术说明：
    1. 程序会自动检测图像类型，目前支持JPG/TIFF/RAW等图像的格式检测；
    2. 支持带目录路径的文件名，如可以直接指定文件和路径：
       image-rename -b  ~/DCIM/101GEDSC/*
    3. 能正确识别包含空格的文件名；


* 例2(已完成):更改上面的THM图像的文件名结尾为JPG，方便在手机/平板电脑上查看，
     或者上传到网络相册和QQ空间
 运行：image-rename -j *
 输出示例：
----------------
更改文件名尾部的扩展名为 .JPG ...
1 * ignore: 'directory' is a DIRECTORY (accept FILE only) 
2 * skip: 'GEDC0001.JPG'
3 * rename: GEDC0001.THM -> GEDC0001.THM.JPG  [ OK ] 
4 * skip: 'GEDC0001.THM.zip' (never rename an archive file) 
----------------

 技术说明：
    1. 出于文件名安全考虑，结合实际使用情况，本程序会自动识别并跳过目录和压缩文件，
       不会对目录名和压缩文件作执行任何重命名操作；
    2. 如果文件名没有扩展名，或只有一个扩展名，程序会自动在末尾添加新的扩展名JPG，如：
       GEDC0002 -> GEDC0001.JPG 
       GEDC0001.THM -> GEDC0001.THM.JPG 
    3. 如果文件名有2个或更多的扩展名，程序会自动把末尾的扩展名改为JPG


* 例3(已完成):把例2中的THM图像扩展名改回原始文件名
 运行：image-rename -s THM *THM*
 输出示例：
----------------
1 * rename: GEDC0001.THM.JPG -> GEDC0001.THM  [ OK ] 
2 * skip: 'GEDC0001.THM.zip' (never rename an archive file) 
----------------


* 例4(已完成):在文件名前面自动添加文件的修改日期
 运行：image-rename -d *
 输出示例：
----------------
1 * ignore: 'directory' (is a DIRECTORY, but accept FILE only)
2 * rename: 'GEDC0001.JPG' -> ./2014-03-10_GEDC0001.JPG  [ OK ]
3 * rename: 'GEDC0001.THM' -> ./2014-03-10_GEDC0001.THM  [ OK ]
4 * rename: 'GEDC0001.THM.zip' -> ./2014-03-10_GEDC0001.THM.zip  [ OK ]
----------------


* 例5(已完成): 在文件名前面自动添加指定文字

 运行：image-rename -p 杭州 *
 输出示例：
----------------
在文件名前面添加文字...
1 * 重命名: '2014-01-01_' -> '杭州2014-01-01_' 	[ OK ]

2 * 忽略: 'DIR'	(忽略目录, 只支持文件操作)
3 * 重命名: 'GEDC1.jpg' -> '杭州GEDC1.jpg' 	[ OK ]
4 * 重命名: 'GEDC1314.jpg' -> '杭州GEDC1314.jpg' 	[ OK ]
5 * 重命名: 'GEDC2.jpg' -> '杭州GEDC2.jpg' 	[ OK ]
6 * 重命名: 'image-rename.jpg' -> '杭州image-rename.jpg' 	[ OK ]
7 * 重命名: 'README.THM.txt' -> '杭州README.THM.txt' 	[ OK ]

8 * 错误: 'readme.txt'	(文件未找到，或者不可用)
9 * 重命名: 'test.tar.gz' -> '杭州test.tar.gz' 	[ OK ]
----------------

* 例6(已完成):清除文件名中包含的日期（如发现相机的拍照日期设置错误）

 运行：image-rename -rd *
 输出示例：
----------------
移除文件名里的日期文字（“年年年年-月月-日日_”格式）...
1 * 重命名: 2014-03-10_GEDC0001.JPG -> ./GEDC0001.JPG
2 * 重命名: 2014-03-10_GEDC0001.THM -> ./GEDC0001.THM
3 * 重命名: 2014-03-10_GEDC0001.THM.zip -> ./GEDC0001.THM.zip

4 * 忽略目录(只支持文件操作): 'directory'
----------------


* 例7(已完成):去掉已添加的文件名前面的文字
 运行：image-rename -rmp GEDC *
 输出示例：
----------------
清除文件名前面的指定文字头...
  原文件名字头: 'GEDC'

1 * 忽略: '2014-01-01_'

2 * 忽略: 'DIR'	(忽略目录, 只支持文件操作)
3 * 重命名: 'GEDC1314.jpg' -> '1314.jpg' 	[ OK ] 
4 * 重命名: 'GEDC1.jpg' -> '1.jpg' 	[ OK ] 
5 * 重命名: 'GEDC2.jpg' -> '2.jpg' 	[ OK ] 
6 * 忽略: 'image-rename.jpg'
7 * 忽略: 'README.THM.txt'
8 * 错误: 'readme.txt'	(文件未找到，或者不可用)
9 * 忽略: 'test.tar.gz'
----------------


* 例8(已完成):改变/替换文件名前面的文字，改为其它相机的文件名编
   号规则如把原通用相机的 GEDC****.JPG 格式文件名，改为
   三星相机的 SSM*****.JPG 格式文件名

   参考运行参数：image-rename -rpp GEDC SSM0 *
输出示例：
----------------
替换文件名前面的指定文字头...
  原文件名字头: 'GEDC'
  新文件名字头: 'SSM0'

1 * 忽略: '2014-01-01_'

2 * 忽略: 'DIR'	(忽略目录, 只支持文件操作)
3 * 重命名: 'GEDC1314.jpg' -> 'SSM01314.jpg' 	[ OK ] 
4 * 重命名: 'GEDC1.jpg' -> 'SSM01.jpg' 	[ OK ] 
5 * 重命名: 'GEDC2.jpg' -> 'SSM02.jpg' 	[ OK ] 
6 * 忽略: 'image-rename.jpg'
7 * 忽略: 'README.THM.txt'
8 * 错误: 'readme.txt'	(文件未找到，或者不可用)
9 * 忽略: 'test.tar.gz'
----------------

* 例9(已完成):去除JPG图像中的EXIF元数据，而不是只改变文件名

 说明：本选项只清除JPG/TIF/RAW图像文件的EXIF元数据，处理后另存为
    "原文件名.noexif.扩展名"，原始文件不会做任何删除或更改，
    也不会对压缩文件或其它格式文件执行任何操作。 
 技术原理：运行时调用 imagemagick 的 “convert -strip”命令和参数。
    详细操作见后面《附录1》。

 命令：image-rename --noexif ~/DCIM/*/*
 输出示例：
----------------
移除JPG/RAW/TIFF图像的EXIF元数据...

1 * 忽略: '/home/user/DCIM/101GEDSC/DIR'	(忽略目录, 只支持文件操作)
2 * 另存为: '/home/user/DCIM/101GEDSC/GEDC0001.JPG' -> 'GEDC0001.JPG.noexif.JPG' 	[ OK ] 
3 * 另存为: '/home/user/DCIM/101GEDSC/GEDC0001.THM.JPG' -> 'GEDC0001.THM.JPG.noexif.JPG' 	[ OK ] 
4 * 另存为: '/home/user/DCIM/101GEDSC/GEDC0002.JPG' -> 'GEDC0002.JPG.noexif.JPG' 	[ OK ] 
5 * 另存为: '/home/user/DCIM/101GEDSC/image-rename.jpg' -> 'image-rename.jpg.noexif.jpg' 	[ OK ] 
6 * 另存为: '/home/user/DCIM/101GEDSC/IMG_20140214_201314.jpg' -> 'IMG_20140214_201314.jpg.noexif.jpg' 	[ OK ] 
7 * 忽略: '/home/user/DCIM/101GEDSC/README.txt'	(未知的文件格式，或者文件不可用)
8 * 忽略: '/home/user/DCIM/101GEDSC/test.tar.gz'	(不会对压缩文件进行操作)

---------------

提示：清除EXIF元数据后，保存的图像文件的修改时间会变成当前时间，
   如果这时使用 image-rename -d 参数来以日期重命名文件名，可能
   执行结果与期望不符。建议有需要的用户，请先运行 -d 参数改变图像
   文件名，然后再运行 --rmexif 来清除 EXIF 元数据。


=========================================

附：如何在Linux下清除JPG图像的EXIF元数据

    目前有2种比较实用的方法，只要在命令行下输入相关命令和参数即可。

  * 附录1：使用 imagemagick 软件包的 convert 命令清除JPG图像的EXIF元数据

    资料来源：
        http://demi-panda.com/2012/12/04/linux-imagemagick/

	使用 imagemagick 命令去除JPEG图像多余的Exif信息

	    Exif信息是数码相机在拍摄过程中采集的一系列信息，这些信息放置
	在我们熟知的jpg文件的头部，也就是说Exif信息是镶嵌在JPEG图像文件
	格式内 的一组拍摄参数，主要包括摄影时的光圈、快门、ISO、日期时间
	等各种与当时摄影条件相关的讯息，相机品牌型号，色彩编码，拍摄时录
	制的声音以及全球定位 系统（GPS）等信息。简单的说，它就好像是傻瓜
	相机的日期打印功能一样，只不过Exif信息所记录的资讯更为详尽和完备。
	不过，具有Exif信息的 JPEG图像文件要比普通的JPEG文件略大一点。
	还有就是像PS这种软件处理过的图像会有"program comments"。
	如果不是专业的摄影类网站，这些信息是没有用的，可以去掉：

	convert -strip input.jpg output.jpg

	命令语法解释：
	  input.jpg  指原始图像文件
	  output.jpg 指另存为的文件名
--------------------

  * 附录2: 使用 exiftool 命令清除JPG图像的EXIF元数据

	资料来源：
	http://www.guokr.com/article/6719/

	Linux用户需要下载一叫做EXIFTool的软件。
	这份软件也同样适用于Windows和Mac操作系统，但使用起
	来比上述方法要复杂些。
    	在Linux环境下，你可以输入下面这个语句来把这个软件安装到
	Ubuntu上：

	sudo apt-get install libimage-exiftool-perl

	要清除exif信息，只需把工作目录改变为目标图像的文件夹，然后输入语句：

	exiftool -all= *.jpg

	这一指令也会把所有参与处理的图像复制一份，并在原图的名称上加上
	后缀_original用以区别。
