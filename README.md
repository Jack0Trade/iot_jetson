# iot_jetson

Install Serial-To-USB Driver:
Add serial-to-usb driver to establish communication between Jetson device and micro-controller:

# Remove BRLTTY, which can cause conflicts with serial devices
sudo apt remove --purge -y brltty
# Install the Python library 'pyserial' for serial communication
pip install pyserial
# Update package lists and install Git
sudo apt-get update
# Install Git, a version control system used for tracking changes in source code
sudo apt-get install -y git
# Clone the CH341SER repository, which contains the driver source code
git clone https://github.com/juliagoda/CH341SER
# Navigate to the cloned repository
cd CH341SER
# Compile the CH341SER driver
make
# Load the compiled driver into the kernel
sudo make load
# Copy the compiled driver to the system modules directory
sudo cp ch34x.ko /lib/modules/$(uname -r)/kernel/drivers/usb/serial/
 # Update module dependencies to include the new driver
sudo depmod -a
# Add the driver to the list of modules to load at boot
echo "ch34x" | sudo tee -a /etc/modules
# Reboot the system to apply changes
sudo reboot
How to Set Up the Project
Clone the Repository:

Run the following command in your terminal:
git clone https://github.com/theniceduck/jetson-iot.git
Rename and Update the Configuration File:

Rename config.h.example to config.h:

mv esp32/config.h.example esp32/config.h
Open config.h in a text editor and fill in the necessary details as per your project requirements.

Upload esp32/esp32.ino to the ESP32 device.

Install Docker and Docker Compose:

For Windows and Mac, download and install Docker Desktop.
For Linux, install Docker and Docker Compose using your package manager. For example, on Ubuntu:
sudo apt-get update
sudo apt-get install docker.io docker-compose
Ensure Docker is set to use the WSL2 based engine if you are on Windows.
Run the Application:

Navigate to the project directory in your terminal and run:
docker-compose up -d --build
# If using the Compose plugin, use the following command:
docker compose up -d --build
Enjoy:

Your application should now be running. Access it via the specified ports in docker-compose.yaml file.
Manage Docker Containers:

To stop the running containers momentarily, use the following command:
docker-compose stop
To remove the container along with its associated volumes, use:
docker-compose down -v
This command will stop the containers and remove them, along with any volumes defined in the docker-compose.yaml file.
How to Use YOLOv8 Object Detection
Set Execute Permissions:
Right-click on ./yolo/create_venv.sh and ./yolo/start.sh to give permission to execute as a program.
Create the Virtual Environment:
Right-click on create_venv.sh and select "Run as program" to create the virtual environment and install the required packages.
Start the YOLOv8 Detection:
Right-click on start.sh and select "Run as program" to start the YOLOv8 object detection.
