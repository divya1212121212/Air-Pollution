# Air-Pollution
# Import necessary libraries
import time
import serial

# Set up serial connection (replace 'COMx' with your Arduino's serial port)
ser = serial.Serial('COMx', 9600, timeout=2)

def read_sensor_data():
    # Read data from the gas sensor
    ser.write(b'R')  # Send 'R' to request data
    time.sleep(1)    # Wait for the sensor to respond
    response = ser.readline().decode('utf-8').strip()

    return response

def main():
    try:
        while True:
            sensor_data = read_sensor_data()
            print(f"CO Level: {sensor_data} ppm")

            # You can add logic here to send data to a cloud platform or perform other actions

            time.sleep(5)  # Adjust the sleep time based on your needs

    except KeyboardInterrupt:
        ser.close()

if __name__ == "__main__":
    main()
