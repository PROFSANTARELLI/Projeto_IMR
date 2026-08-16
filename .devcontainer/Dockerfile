FROM althack/ros2:humble-dev

# Instalar pacotes essenciais, simuladores, ferramentas de GUI e noVNC
RUN apt-get update && apt-get install -y \
    ros-humble-desktop \
    ros-humble-turtlebot3 \
    ros-humble-turtlebot3-gazebo \
    ros-humble-turtlebot3-simulations \
    ros-humble-gazebo-ros-pkgs \
    python3-colcon-common-extensions \
    python3-pip \
    novnc \
    websockify \
    x11vnc \
    xvfb \
    fluxbox \
    && rm -rf /var/lib/apt/lists/*

# Configurar modelo padrão do TurtleBot3
ENV TURTLEBOT3_MODEL=burger

# Script de inicialização da interface gráfica web (noVNC na porta 6080)
RUN echo '#!/bin/bash\n\
export DISPLAY=:1\n\
Xvfb :1 -screen 0 1280x720x24 &\n\
sleep 1\n\
fluxbox &\n\
x11vnc -display :1 -nopw -forever -shared &\n\
websockify --web /usr/share/novnc/ 6080 localhost:5900 &\n\
bash' > /usr/local/bin/start-vnc.sh && chmod +x /usr/local/bin/start-vnc.sh
