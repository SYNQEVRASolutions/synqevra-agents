# Compressor Health Agent

An AI agent for **air compressor monitoring and predictive maintenance**. It reads the telemetry your compressor controller already exposes, learns what normal looks like for that unit at that site, and sends one alert per incident with what failed, what is affected, how urgent it is, and what to do next.

Part of the [SYNQEVRA Agents](../..) index by [SYNQEVRA Solutions](https://github.com/SYNQEVRASolutions).

## The problem

A compressor does not usually fail without warning. Discharge temperature creeps up. Oil pressure drifts. Loading cycles get shorter. Moisture in the line rises slowly after a dryer starts to lose efficiency.

None of that trips an alarm, because nobody set a threshold for a number that moves 2 percent a week. What actually alarms is the shutdown, and by then production has stopped.

## What it does

1. **Reads** the metrics a typical controller or gateway publishes: discharge temperature, oil pressure, sump pressure, motor current, load and unload cycles, running hours, dew point where a dryer is present.
2. **Learns a baseline** per unit per shift, so "normal" is compared against this compressor's own history, not a generic datasheet number.
3. **Detects drift** and classifies it: thermal, lubrication, load behaviour, or moisture. Slow trends are reported as trends, not as alarms.
4. **Sends one alert per incident** with four fields an operator can act on: what failed, what is affected, how urgent, what to do now. Repeated alarms for the same cause are folded into one.

## How it runs

1. Collect from the controller over Modbus TCP, SNMP, OPC UA, or your existing gateway, on a 30 to 60 second poll.
2. Store a rolling baseline locally, typically 14 to 30 days depending on shift patterns.
3. Score each cycle and raise an alert when a metric moves outside its learned band or when a trend holds for longer than the expected settling time.

It runs beside your existing control system. It does not write to the compressor and it does not replace the safety interlocks.

## Integrations

Modbus TCP, SNMP v2c and v3, OPC UA, MQTT, and HTTP pull where a vendor gateway only offers a JSON endpoint. Alerts go out by email, WhatsApp, Slack, or into an existing ticketing tool.

## Deployment

A single-site install is usually **3 to 5 working days** from data access to live alerts: one day to read the points list, two to three days to build and tune the baseline, one day for sign-off. Multi-site rollouts follow the same pattern per site.

## Pricing

Starting from a fixed scoped build, priced per site and per number of monitored assets. Monitoring and tuning after go-live is a monthly line item, not a surprise. Contact us with the asset count and the protocol your controllers speak and you get a number, not a range.

## Contact

- Email: fatircompanyai@gmail.com
- Organisation: [github.com/SYNQEVRASolutions](https://github.com/SYNQEVRASolutions)

If your plant, data center or workshop needs this, contact SYNQEVRA Solutions.
