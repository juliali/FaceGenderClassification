训练自己的人连性别分类模型

1. 创建gender_solver.prototxt, gender_train_val.prototxt等文件，存储到configfiles目录下

2. 将所有作为输入数据的人脸图片以jpg格式存储到 images目录下

3. 生成train.txt文件，这个文件包括两列，一列是图片文件名（不需要带路径），另一列是性别标志，0代表男，1代表女。	

4. 安装caffe，具体方法参见：
http://caffe.berkeleyvision.org/installation.html

5. 运行下列命令来训练模型

（1） ${caffe_root_path}\convert_imageset.exe --resize_height=600 --resize_width=600 --shuffle ${fcc_root_path}\images\ ${fcc_root_path}\configfiles\train.txt ${fcc_root_path}\gender_train_lmdb
（2） ${caffe_root_path}\compute_image_mean.exe ${fcc_root_path}\gender_train_lmdb ${fcc_root_path}\configfiles\mean_image.binaryproto
（3） ${caffe_root_path}\caffe.exe train --solver ${fcc_root_path}\configfiles\gender_solver.prototxt

e.g.: caffe_root_path = c:\projects\caffe\build\tools\Release
	  fcc_root_path = c:\projects\github\facegenderclassification

train程序每迭代1000次，就会有一个模型文件，名为：caffenet_train_iter_${iter_number}.caffemodel，生成在${facc_root_path}目录下
