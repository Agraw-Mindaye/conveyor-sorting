# Conveyor Sorting PLC

## Overview
A PLC-based converyor system that sorts items into trays (A/B) using a
diverter. The system runs one item at a time and enforces a route-dependent tray-empty interlock:
  the conveyor will only transfer an item if its destination tray is empty

## Key Behaviors
- Safe startup: no automatic motion on power-up
- Route latched per item on infeed detect
- Route-dependent tray-empty permissive (A requires Tray A empty, B requires Tray B empty)
- Faults are latched and require local reset; after reset the system returns to STOPPED

## State Machine
STOPPED → IDLE_READY → (WAIT_TRAY_EMPTY) → TRANSFER → IDLE_READY  
Any fault → FAULT (latched) → RESET → STOPPED

## Contents
- `docs/` Control philosophy, I/O list, state machine, fault handling
- `codesys/` CODESYS project files
- `exports/` PLCopen + native XML exports for diff/review
- `media/` Diagrams and screenshots

## Tools
- CODESYS V3
- (Optional) Factory I/O / simulation environment
