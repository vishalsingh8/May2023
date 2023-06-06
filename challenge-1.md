# Data Packet Corruption Detection
* In a Wireless communciation device, multiple data packets are transferred over the air. 
* It is possible that data might get corrupted or lost before it reaches the destination.
* Create a method to identify if a data packet is corrupted
* Assume below format for the data packet

```
#include <stdint.h>

#define MAX_PACKET_DATA_LENGTH (50)

typedef struct data_packet_t {
    uint8_t id;
    uint8_t data_length;
    uint8_t data[MAX_PACKET_DATA_LENGTH];
    uint16_t crc;
} data_packet_t;

uint16_t calculateCRC(const uint8_t* data, uint8_t length) {
    // CRC calculation implementation
    // You can use a standard CRC algorithm like CRC-16
    // There are several implementations available online
    // Here's a simple example using CRC-16-CCITT:
    const uint16_t crcTable[256] = {
        // CRC table values
    };

    uint16_t crc = 0xFFFF;
    for (uint8_t i = 0; i < length; i++) {
        crc = (crc >> 8) ^ crcTable[(crc ^ data[i]) & 0xFF];
    }

    return crc;
}

int isPacketCorrupted(const data_packet_t* packet) {
    // Calculate the CRC of the received packet data
    uint16_t calculatedCRC = calculateCRC(packet->data, packet->data_length);

    // Compare the calculated CRC with the received CRC
    if (calculatedCRC == packet->crc) {
        // Packet is not corrupted
        return 0;
    } else {
        // Packet is corrupted
        return 1;
    }
}

# FAQ's
* Links to Discussions
