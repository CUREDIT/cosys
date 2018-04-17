**<h3>M 1. Agent based Control structures</h3>**

'Don't just control it, [Co]control it'

This interface is a plan for one week's work but a long term time saver:<br/>
<b>[CoSys]</b>control server will provide the following style of command line APIs for in-network device management

```$ agents ag AND controls cg OR capabilities sg AND schedules hg```

The interface simply asks for 
 - one agent or an agents' groups and 
 - what they must do based on the control or the controls' groups


<h4>API Structure: </h4>

[TODO improve examples, preview + annex section]

**- Level 1. Devices - Controls**<br/>
**- Level 2. Devices - Controls - Services**<br/>
**- Level 3. Devices - Controls - Services - Schedules**<br/>

Examples:

**Level 1.** One or more devices in a collection can be configured by a manager by writing a statement like:

```TVs[pax, quarantine, location-deck] play[multicast, udp://239.11.21.23:4000] as myCurrentChannel```

**Or a user could issue commands that basically comes down to running the following API call**

```TV display[app-payments]```<br/>
```TV make[reservations-LAUFAUF]```

**Level 2.** Besides ```play[multicast]``` you could add

```run[muting_service, volume_manager, internet_plans_service]```<br/>
```clean[logs]```<br/>
```test[connection[test-command-list] between[TV, LGServer]]```

**Level 3.** Besides verb controls with noun services, allow piping processes to temporal schedulers like

```TV play[my-daily-movie | every[day from[2000] to[2200]]]```<br/>
```run [clean[logs] | every[day at[default-time]]]```<br/>

**or causal schedulers like**

```TVs play[mustering-channel-3 | when[emergency-alert-!]]```<br/>
```TVs display[app-survey | after[event-shorex]]```<br/>
```TV display[app-payments | after[casino-visit]]```<br/>
```TV reserve[LAUFAUF for[dinner] for[2] | every[day at[2100]]]```<br/>


<h4>API Interactions:</h4>
 [TODO improve examples, preview + annex section]

**Controls belong to agents and have associated capabilities and schedules.**

After typing the id of an agent or an agent group, a control or group of controls are shown.<br/>
After selecting the controls, an advanced user may still choose to specify capabilities specifically <br/>
or, skip user interactions entirely and just provide capabilities and their schedules.

**Capabilities are derived from controls and controls and controls are derived from agents.** 

```$ Agents ag && Controls cg || (Capabilities sg && Schedules hg)```<br/>
```$ Agents ag && (Controls cg || Capabilities sg) && Schedules hg```

For this we will need to hide all the internal complexity and latencies in the multi-server network.<br/>

**<h3>M 2. Unified Access Interface</h3>**

For a unified API we need

**- a separation of concerns between business logic, caching and persistence**

**- a single source of truth for all clients in the system.**

**- agent driven, supervised state machines (e.g. interceptions vs polling)**

**- asynchronous abstract annotations exchanges**

**- a network as concepts**

**Demo Showcase**: Composing business-ready, smart contracts, permissions and identification based blockchain network applications on the fly.

But 'blockchain' is just one of the small pieces. <br/>
One can **generate a unified access interface and the single source of truth for any organization's network**.

**<h3>M 3. Separation of caching,  persistence and business logic</h3>**
+(ttl, ssot snapshots standards)

**<h3>M 4. Exchanging annotated abstract codes instead of just static assets</h3>**
+(BNA, smart contract standards)

**<h3>M 5. Agent driven, supervised  state machines</h3>**
+(e.g. interceptors instead of long polling, supervised state transitions)
