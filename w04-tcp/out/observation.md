# Observation

## Task 1
- I chose stop-and-wait because the simulated channel reorders, drops, and duplicates packets; with a single in-flight segment the protocol is easy to reason about and still passes both seeds.
- The channel carried 3,047 packets for 2,000 bytes of payload on seed 246, while the minimum reliable path is roughly 250 data packets plus ACKs, so the reliability overhead is large but stable under loss and duplication.
- The first failure mode was loss, then reordering: repeated retransmission fixed the missing segments, while duplicate data and ACKs were ignored by checking the sequence number before accepting the payload.

## Task 2
- The capture used SYN sequence 123456789 and SYN-ACK sequence 234567890; TCP does not start at zero because each side chooses a random initial sequence number for the connection.
- The scaled receive window is 65,535 << 7 = 8,388,480 bytes, but the transfer never filled that window; the system was limited by the network path and handshake timing rather than the receiver buffer.
- The two medians were 183.05 Mbps on campus Wi‑Fi and 166.66 Mbps on tethering, with spreads of 23% and 61%; the worse handshake time directly lowers throughput because the RTT and congestion window are coupled.

## Task 3
- The baseline has the highest goodput because it keeps its fixed window full, but it is still the worst sender because it fills the queue to the drop point and throws away a large share of traffic.
- The controller uses slow start followed by additive increase, with a gentler 25% backoff after loss; it settles near the pipe limit of roughly 20 packets and keeps the average queue around 4.3.
- That trade-off costs a little goodput versus the raw baseline, but it keeps loss below 1% and queue below 5.0, which is what makes the link behave well for everyone sharing it.
