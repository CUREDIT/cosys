**M 1. Agent based Control structures**

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

```TVs[pax, quarantine, location-casino-1] play[multicast, udp://239.11.21.23:4000] as myCurrentChannel```

**Or a user could issue commands that basically comes down to running the following API call**

```TV display[app-payments]```<br/>
```TV make[reservations-LAUFAUF]```

**Level 2.** Besides ```play[multicast]``` you could add

```run[muxing_service, volume_manager, internet_plans_service]```<br/>
```clean[logs]```<br/>
```test[connection[test-command-list] between[TV, GameServer]]```

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

**M 2. Unified Access Interface**

For a unified API we need

**- a separation of concerns between business logic, caching and persistence**

**- a single source of truth for all clients in the system.**

**- agent driven, supervised state machines (e.g. interceptions vs polling)**

**- asynchronous abstract annotations exchanges**

**- a network as concepts**

**Demo Showcase**: Composing business-ready, smart contracts, permissions and identification based blockchain network applications on the fly.

But 'blockchain' is just one of the small pieces. <br/>
One can **generate a unified access interface and the single source of truth for any organization's network**.

  - M 3. Separation of caching,  persistence and business logic**
  + (ttl, ssot snapshots standards)

  - M 4. Exchanging annotated abstract codes instead of just static assets**
  + (BNA, smart contract standards)

  - M 5. Agent driven, supervised  state machines**
  + (e.g. interceptors instead of long polling, supervised state transitions)


**M 3. Single Source of Truth as a Service**

This section assumes that your system already has sufficiently abstracted away its transport problems. If your existing design is still not transport mode agnostic please refer to previous milestones.

**Events**:

 - An initial handshake and a final goodbye are special events that override or delete all other events.

 - Upon initial handshake with the Control server, an agent receives a state or an event or an event-state map.

 - Only events - not agents directly - can alter state. Control server handshakes and conversations are special events


**Agents**:

 - Every n seconds after initial handshake, the expected end state (which has values and other states) is shared to the Control server client.

 - Every temporal agent gets a state update as a state diff or an event diff or an event-state map diff or a ‘nodiff’ (or 404 if not using a messaging layer).

 - Every agent may request diffs any time necessary (e.g. based on the agent’s internal event-state transforms) and receive a diff promise or a nodiff/404.


**States**:

 - Every agent has real time access to every other agent’s states.
 - Event dispatchers and listeners may be private or shared within an agent group.
 - A group of such event handlers form a control group.
 - State transforms happen via agents or controls or capabilities or schedules.
 - After the final goodbye or expiration of TTL, the shared state becomes invalid.

- in the canonical device - user 2-agent systems:

  - Device state changes are available to the user’s remote control in real time (without the user’s remote control having to make a call     to the device).

  - User state changes change corresponding device state on all the user’s devices in real time (without the user having to refresh or       make a call to the device).


**SSOT Cache**:

SSOT as a Service requires all necessary data to be always pre-fetched from the database(s) with only the most updated version of the data available to the user.

- Every database and/or data source must have CRUD interceptors that dispatch entity CRUD events to the SSOT Cache provider.
- Clients do not get data and state maps from the databases or the servers using the databases but rather exclusively from SSOT as a Service provider.
- Especially for systems without permanent storage services, SSOT Cache snapshots will be made according to that system’s snapshot schedulers that belong to either temporal or causal snapshot agents
