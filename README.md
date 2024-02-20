# Wishing Well API Documentation

<img src="https://github.com/elwellb/WishingWell/blob/main/project_sketch.webp?raw=true" width="500">

## Overview

This API documentation describes the OSC (Open Sound Control) messages supported by our project for interacting with wish lists, images, and a motor-controlled crank mechanism. OSC is a protocol for networking sound synthesizers, computers, and other multimedia devices for purposes such as musical performance or show control.

## OSC Address Spaces

The project supports the following OSC address spaces for communication:

### `/wish_list`

- **Direction**: Outbound (Publish)
- **Description**: This topic publishes updates to the wish list. Any time the wish list is updated, a message is sent to subscribers with the current list of wishes.
- **Message Format**: A string list, each element representing a wish.
- **Example Message**: `["Wish 1", "Wish 2", "Wish 3"]`

### `/image`

- **Direction**: Outbound (Publish)
- **Description**: This topic publishes the latest generated image. Whenever a new image is available, a message containing the image data is sent.
- **Message Format**: Binary blob of the image data, typically encoded in a common format such as JPEG or PNG.
- **Example Message**: Binary data representing the image.

### `/crank`

- **Direction**: Inbound (Receive)
- **Description**: Receives a command to move the crank to a specified position. The position is controlled by a motor based on the received value.
- **Message Format**: A single float value representing the desired position of the crank.
- **Example Message**: `0.75` (Indicates the crank should move to 75% of its range.)

## Communication Protocols

- **Port**: Ensure that your OSC client is configured to communicate on the correct port. The specific port number used by the project should be documented and provided to all developers.
- **IP Address**: The IP address of the device or server where the OSC messages are being sent to or received from must be known and reachable within your network.

## Implementation Notes

- **Rate Limiting**: Be mindful of the rate at which you send OSC messages, especially for the `/crank` topic, to prevent overwhelming the motor controller.
- **Data Encoding for `/image`**: Images should be properly encoded and tested to ensure compatibility across different systems receiving the OSC messages.
- **Error Handling**: Implement appropriate error handling for situations where messages are malformed or cannot be delivered.

## Getting Started

To start interacting with the project using OSC messages:

1. Configure your OSC client with the project's IP address and port.
2. Subscribe to the `/wish_list` and `/image` topics to receive updates.
3. To control the crank, send messages to the `/crank` topic with the desired position value.
