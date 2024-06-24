# PRE INSTALLATION
![image](https://github.com/rocky-2904/PRODIGY_CS_05/assets/173170607/38dcaa1c-1937-42b9-bf70-0b49cdc991ef)

# And before performing your coding you must install Wimpcp or npcap
# WIMPCAP INSTALLATION 
![image](https://github.com/rocky-2904/PRODIGY_CS_05/assets/173170607/48f3a796-b115-490f-a2f4-c858366a0a93)
# NPCAP INSTALLATION
![image](https://github.com/rocky-2904/PRODIGY_CS_05/assets/173170607/4edf4646-5646-420c-947d-97d40ebaa2fe)

# CODE                  
    import scapy.all as scapy

    def packet_callback(packet):
      if packet.haslayer(scapy.IP):
        src_ip = packet[scapy.IP].src
        dst_ip = packet[scapy.IP].dst
        protocol = packet[scapy.IP].proto

        print(f"Source IP: {src_ip} | Destination IP: {dst_ip} | Protocol: {protocol}")

        if packet.haslayer(scapy.TCP):
            try:
                payload = packet[scapy.Raw].load
                decoded_payload = payload.decode('utf-8', 'ignore')
                print(f"TCP Payload")
            except (IndexError, UnicodeDecodeError):
                print("Unable to decode TCP payload.")

        elif packet.haslayer(scapy.UDP):
            try:
                payload = packet[scapy.Raw].load
                decoded_payload = payload.decode('utf-8', 'ignore')
                print(f"UDP Payload")
            except (IndexError, UnicodeDecodeError):
                print("Unable to decode UDP payload.")

    def start_sniffing():
      scapy.sniff(store=False, prn=packet_callback)

    start_sniffing()
