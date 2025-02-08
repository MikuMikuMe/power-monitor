# power-monitor

Creating a real-time power consumption monitoring system using IoT devices involves various components. For simplicity, we'll create a basic Python program that simulates the collection and monitoring of power consumption data. We'll use local data and libraries to simulate IoT functionality. In a real-world application, you might connect this to a database, cloud service, or IoT hardware.

Below is a complete Python program that demonstrates a basic simulation:

```python
import time
import random
import logging

# Configure logging
logging.basicConfig(level=logging.INFO, format='%(asctime)s - %(levelname)s - %(message)s')

class PowerMonitor:
    def __init__(self):
        self.devices = ["Device1", "Device2", "Device3"]
        self.consumption_data = {device: [] for device in self.devices}

    def simulate_power_consumption(self):
        """
        Simulates real-time power consumption data for each device.
        """
        try:
            for device in self.devices:
                # Simulate random power consumption between 100 and 500 Watts
                power_usage = random.randint(100, 500)
                self.consumption_data[device].append(power_usage)
                logging.info(f"Recorded power consumption for {device}: {power_usage}W")
        except Exception as e:
            logging.error("Error simulating power consumption: %s", str(e))

    def get_average_consumption(self, device):
        """
        Calculate the average power consumption for a given device.

        Parameters:
        device (str): The device name to calculate average consumption for.

        Returns:
        float: Average power consumption.
        """
        try:
            if device not in self.consumption_data:
                raise ValueError(f"Device {device} not found.")

            data = self.consumption_data[device]
            if not data:
                return 0.0

            average = sum(data) / len(data)
            logging.info(f"Average power consumption for {device}: {average}W")
            return average
        except Exception as e:
            logging.error("Error calculating average consumption: %s", str(e))
            return 0.0

    def monitor(self, duration=10):
        """
        Monitor power consumption for a specific duration.

        Parameters:
        duration (int): The number of seconds to monitor power consumption.
        """
        try:
            start_time = time.time()
            while time.time() - start_time < duration:
                self.simulate_power_consumption()
                time.sleep(1)  # Simulate delay between readings
        except Exception as e:
            logging.error("Monitoring error: %s", str(e))

if __name__ == "__main__":
    power_monitor = PowerMonitor()
    power_monitor.monitor(duration=10)  # Monitor for 10 seconds

    for device in power_monitor.devices:
        power_monitor.get_average_consumption(device)
```

### Explanation:
- **Logging:** The program uses Python's `logging` library for logging events. It's configured to output info-level logs with timestamps.
- **Simulation:** The `simulate_power_consumption` function generates random power usage values for each device at each interval.
- **Average Calculation:** The `get_average_consumption` function calculates the average power consumption for a given device and includes basic error handling.
- **Monitoring Logic:** The `monitor` method runs the simulation over a specified period (defaulting to 10 seconds).

### Error Handling:
- The code includes several try-except blocks that log errors if any exceptions occur during simulation or calculations.

The above code simulates data generation and processing. For actual IoT integration, you'll need:
- Connectivity to IoT devices over a network.
- Real sensors to collect consumption data.
- Data storage or an external service for real-time analysis.

The program as written is extendable and can serve as a starting point for additional data handling and analysis logic.