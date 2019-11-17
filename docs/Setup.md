# Настройка окружения
В данном руководстве описано, как настроить рабочее окружение для работы с turtlebot3 в Gazebo симуляции. 

##### 1. Установка ubuntu 16.04

Сначала качаем образ. Рекомендую ubuntu 16.04.6 с графической оболочкой LXDE [скачать с официального сайта](http://cdimage.ubuntu.com/lubuntu/releases/16.04/release/lubuntu-16.04.6-desktop-amd64.iso)

Потом записываем образ на флешку и устанавливаем, используя [величайший сайт](google.com) и [не менее великий сайт](https://losst.ru/ustanovka-linux-ryadom-s-windows-10)

> Важно выполнить обновление системы после установки, поэтому ОБЯЗАТЕЛЬНО пропишите следующие команды в терминале. 

```bash
sudo apt update -y && sudo apt upgrade -y && sudo apt dist-upgrade -y && sudo apt autoremove -y
```

> P.S. Прописывайте это в терминале после каждого запуска linux, чтобы отсутствие обновлений не обрушило вам иксы [лулзы](http://lurkmore.to/%D0%9F%D0%BB%D0%B0%D0%B7%D0%BC%D0%B0_%D0%BD%D0%B5_%D0%BF%D0%B0%D0%B4%D0%B0%D0%B5%D1%82). Да, отчасти из-за этого я рекомендую LXDE. У вас ничего не упадёт, если нет графических финтифлюшек. 

##### 2. Установка ROS

Для ubuntu 16.04 доступен [ROS kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu). Для особенно ленивых вот готовая последовательность bash команд для установки полной версии.

```bash
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

sudo apt-get update

sudo apt-get install ros-kinetic-desktop-full

sudo rosdep init
rosdep update

echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc

sudo apt install python-rosinstall python-rosinstall-generator python-wstool build-essential

mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
cd ~/catkin_ws
catkin_make


!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!


echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
echo "source ~/StarLine_Hackathon/catkin_ws/devel/setup.bash" >> ~/.bashrc
echo "export TB3_MODEL=\"waffle\"" >> ~/.bashrc
echo "export TURTLEBOT3_MODEL=${TB3_MODEL}" >> ~/.bashrc
source ~/.bashrc
```

##### 3. Установка пакетов turtlebot3 и симуляции

Подробная документация для работы с turtlebot3 [тут](http://emanual.robotis.com/docs/en/platform/turtlebot3/overview/)

```bash
sudo apt-get install ros-kinetic-joy ros-kinetic-teleop-twist-joy ros-kinetic-teleop-twist-keyboard ros-kinetic-laser-proc ros-kinetic-rgbd-launch ros-kinetic-depthimage-to-laserscan ros-kinetic-rosserial-arduino ros-kinetic-rosserial-python ros-kinetic-rosserial-server ros-kinetic-rosserial-client ros-kinetic-rosserial-msgs ros-kinetic-amcl ros-kinetic-map-server ros-kinetic-move-base ros-kinetic-urdf ros-kinetic-xacro ros-kinetic-compressed-image-transport ros-kinetic-rqt-image-view ros-kinetic-gmapping ros-kinetic-navigation ros-kinetic-interactive-markers

cd ~/catkin_ws/src/
git clone https://github.com/ROBOTIS-GIT/turtlebot3_msgs.git
git clone https://github.com/ROBOTIS-GIT/turtlebot3.git
cd ~/catkin_ws && catkin_make

cd ~/catkin_ws/src/
git clone https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
cd ~/catkin_ws && catkin_make
```

Проверка корректности установки:

```
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

Если на этом этапе вы увидили нечто подобное

![img](images/turtlebot3_world_bugger.png)

Тогда вы всё сделали правильно.

