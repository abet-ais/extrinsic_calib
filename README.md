## Extrinsic Calibration

外部パラメータ推定を行う前に必ず内部パラメータ推定を行うこと  

### 外部パラメータ推定に使うパッケージのインストール
```
sudo apt-get install ros-indigo-checkerboard-detector
```
このパッケージについては [jsk_recognition](http://jsk-docs.readthedocs.io/en/latest/jsk_recognition/doc/checkerboard_detector/index.html) を参考にしてください  

インストールが終わったら
```
roslaunch extrinsic_calib extrinsic_calib.launch
```

チェッカーボードをカメラの視界の中に入れるとキャリブレーションボードからカメラまでのTFが作成される  
```
rosrun tf tf_echo object camera
```
もしくは  
```
rosrun rviz rviz
```
で確認する  

### チェッカーボード(object)からrobot base(世界座標原点) までのTFを作る  
```
roscd extrinsic_calib/launch
emacs extrinsic_calib.launch
```
下の方に書いてある
```
  <node pkg="tf" 
        type="static_transform_publisher" 
        name="waist_to_checkerboard"
        args="0.0875 -0.0903 0.0145 1.5708 0.0 3.1415 /object /robot_base 100" /  >

```
argsに自分で測定したチェッカーボードからロボットベースまでのXYZRPYを入れる  