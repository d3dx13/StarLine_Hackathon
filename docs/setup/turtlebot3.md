# Настройка окружения turtlebot3
В данном руководстве описано, как настроить рабочее окружение для работы с turtlebot3 в Gazebo симуляции. 

##### Установка пакетов turtlebot3 и симуляции

Подробная документация для работы с [turtlebot3](http://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)

```bash
sudo apt-get install ros-kinetic-joy ros-kinetic-teleop-twist-joy ros-kinetic-teleop-twist-keyboard ros-kinetic-laser-proc ros-kinetic-rgbd-launch ros-kinetic-depthimage-to-laserscan ros-kinetic-rosserial-arduino ros-kinetic-rosserial-python ros-kinetic-rosserial-server ros-kinetic-rosserial-client ros-kinetic-rosserial-msgs ros-kinetic-amcl ros-kinetic-map-server ros-kinetic-move-base ros-kinetic-urdf ros-kinetic-xacro ros-kinetic-compressed-image-transport ros-kinetic-rqt-image-view ros-kinetic-gmapping ros-kinetic-navigation ros-kinetic-interactive-markers

cd ~/catkin_ws/src/
git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
cd ~/catkin_ws && catkin_make

cd ~/catkin_ws/src/
git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
cd ~/catkin_ws && catkin_make

echo "export TB3_MODEL=\"waffle\"" >> ~/.bashrc
echo "export TURTLEBOT3_MODEL=${TB3_MODEL}" >> ~/.bashrc
source ~/.bashrc
```

Проверка корректности установки:

```bash
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

Если на этом этапе вы увидели нечто подобное:

![img](images/turtlebot3_world_bugger.png)

Тогда вы всё сделали правильно.

Закрывайте симуляцию путём нажатия ctrl+C в терминале. <u>Это может занять некоторое время.</u>
