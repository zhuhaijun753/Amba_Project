docker环境搭建（docker 用户名：liyunlong 密码：123456）：
    docker load < sdk30.tar
    docker tag [image id] untouch_gele_ubuntu16_v0:baseimage
    docker run -it --user=liyunlong -w /data --name=sdk30_base_image -v /home/liyunlong/work/untouch/linux/sdk3_0_gele_amba_cv25/code/docker_ubuntu:/data --network=host liyunlong_ubuntu1604:sdk30_base_image /bin/bash

    电脑重启后：
    docker restart sdk30_base_image 
    docker exec -it sdk30_base_image /bin/bash

SDK：git clone http://master2/liyunlong/shg_amba_cv25_sdk_3_0_2.git
编译：
      cd shg_amba_cv25_sdk_3_0_2/cv25_linux_sdk_3.0.2/ambarella/boards/cv25_hazelnut
       source build.sh
       make -j8

cnn:
      tar xvfJp cv2x_cnngen_samples_20200928.tar.xz
	  
	  
模型转换：
cv2x_cnngen_samples_20200928
	source build.sh
	make detect_smoke_ox run_mode=layer_compare layer_compare_enable_debug=1 // PC 模拟 输出路径：
	make detect_smoke_ox run_mode=cavalry // board  输出路径：cv2x_cnngen_samples_20200928\out\onnx\test_networks\detect_smoke_ox\cavalry_detect_smoke_ox   图片bin detect_phone_smoke_eura_ox.bin 模型bin detect_smoke_ox_cavalry.bin
	make detect_smoke_ox run_mode=cavalry cavalry_version=2.1.7  // 生成指定版本SDK2.5.X的模型，需要加上参数cavalry_version=2.1.7
	
	test_nnctrl -e -b ./models/detect_smoke_ox_cavalry.bin --in data=./input/detect_smoke.bin --out cls=./out/detect_smoke_ox_cls.bin  --out loc=./out/detect_smoke_ox_loc.bin
	untouch_models_encrypt_tool a.bin a_en.bin //模型加密
	
	