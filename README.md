// Include the necessary libraries
#include <NewPing.h>

// Define the pins for the ultrasonic sensor
#define TRIGGER_PIN  9
#define ECHO_PIN     10

// Define the pins for the motor driver
#define MOTOR_PIN1   2
#define MOTOR_PIN2   3

// Define the maximum distance (in cm) at which the motor should turn on
#define MAX_DISTANCE 20

// Create an instance of the NewPing library for the ultrasonic sensor
NewPing sonar(TRIGGER_PIN, ECHO_PIN);

void setup() {
  // Set the motor pins as output
  pinMode(MOTOR_PIN1, OUTPUT);
  pinMode(MOTOR_PIN2, OUTPUT);
  
  // Turn off the motor initially
  digitalWrite(MOTOR_PIN1, LOW);
  digitalWrite(MOTOR_PIN2, LOW);
  
  // Initialize serial communication for debugging
  Serial.begin(9600);
}

void loop() {
  // Measure the distance using the ultrasonic sensor
  unsigned int distance = sonar.ping_cm();
  
  // Print the distance to the serial monitor for debugging
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  
  // Check if an object is within the specified range
  if (distance < MAX_DISTANCE) {
    // If an object is detected, turn on the motor
    digitalWrite(MOTOR_PIN1, HIGH);
    digitalWrite(MOTOR_PIN2, LOW);
    Serial.println("Motor ON");
  } else {
    // If no object is detected, turn off the motor
    digitalWrite(MOTOR_PIN1, LOW);
    digitalWrite(MOTOR_PIN2, LOW);
    Serial.println("Motor OFF");
  }
  
  // Add a delay to prevent rapid on/off switching (adjust as needed)
  delay(100);
}
