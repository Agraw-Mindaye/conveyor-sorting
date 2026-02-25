
| Current State   | Condition (evaluated each scan) | Next State      | Actions/Notes                                                        |
| --------------- | ------------------------------- | --------------- | -------------------------------------------------------------------- |
| ANY             | `!E_STOP_OK`                    | FAULT           | `FaultLatched := 1` (latched fault), outputs forced safe by defaults |
| STOPPED         | `PB_START && !FaultLatched`     | IDLE_READY      | system becomes ready to accept item                                  |
| IDLE_READY      | `PE_INFEED`                     | WAIT_TRAY_EMPTY | begin processing current item                                        |
| WAIT_TRAY_EMPTY | `!RouteLatched`                 | WAIT_TRAY_EMPTY | `RouteToA := ITEM_TYPE_A; RouteLatched := 1` (latch once)            |
| WAIT_TRAY_EMPTY | `(RouteToA && TRAY_A_EMPTY)     |                 | (!RouteToA && TRAY_B_EMPTY)`                                         |
| TRANSFER        | `clear_rise`                    | IDLE_READY      | stop motor, `RouteLatched := 0` (ready for next item)                |
| FAULT           | `PB_RESET && E_STOP_OK`         | STOPPED         | `FaultLatched := 0; RouteLatched := 0`                               |
