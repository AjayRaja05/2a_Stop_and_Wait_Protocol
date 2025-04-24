# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

import time

import random

class Packet:

    def __init__(self, data, seq_no):
        self.data = data
        self.seq_no = seq_no

    def __str__(self):
        return f"Packet(Data: '{self.data}', Seq: {self.seq_no})"

class Sender:

    def __init__(self, receiver):
        self.receiver = receiver
        self.next_seq_no = 0

    def send(self, data):
        packet = Packet(data, self.next_seq_no)
        print(f"Sender: Sending packet {packet}")
        self.receiver.receive(packet)
        ack = self.wait_for_ack()
        if ack is not None and ack == self.next_seq_no:
            print(f"Sender: Received ACK {ack}. Packet sent successfully.")
            self.next_seq_no = 1 - self.next_seq_no  # Toggle sequence number
            return True
        else:
            print(f"Sender: Timeout or incorrect ACK received ({ack}). Resending...")
            return self.send(data) # Resend the same packet

    def wait_for_ack(self, timeout=2):
        """Simulates waiting for an ACK with a timeout."""
        time.sleep(timeout * random.uniform(0.8, 1.2)) # Simulate network delay
        return self.receiver.acknowledgement

class Receiver:

    def __init__(self):
        self.expected_seq_no = 0
        self.acknowledgement = None

    def receive(self, packet):
        print(f"Receiver: Received packet {packet}")
        if packet.seq_no == self.expected_seq_no:
            print(f"Receiver: Packet received in order. Sending ACK {self.expected_seq_no}")
            self.acknowledgement = self.expected_seq_no
            self.expected_seq_no = 1 - self.expected_seq_no # Toggle expected sequence number
            # Simulate processing the data
            print(f"Receiver: Processing data: '{packet.data}'")
        else:
            print(f"Receiver: Unexpected sequence number. Discarding packet. Sending ACK {1 - self.expected_seq_no} (previous ACK)")
            self.acknowledgement = 1 - self.expected_seq_no # Acknowledge the last correctly received packet

if __name__ == "__main__":

    receiver = Receiver()
    sender = Sender(receiver)

    data_to_send = ["Hello", "World", "This", "is", "Stop", "and", "Wait"]

    for data in data_to_send:
        print("\n--- Sending new data ---")
        sender.send(data)

    print("\n--- Transmission complete ---")
## OUTPUT

![image](https://github.com/user-attachments/assets/89de6cfd-b3ee-4996-8c67-acc2e0197dda)


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
