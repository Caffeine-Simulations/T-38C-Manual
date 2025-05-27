# Navigation

## EGI
### DEST Points
DEST points act as user defined waypoints in the T-38C. They can be steered to by selecting the 3 Digit ID into row 1 of the UFCP using the 3 digit identifier.
!!! Note
    Waypoints with less than 3 digits can be entered with padded zeros. For example:  
    **Waypoint 1:** 001, **Waypoint 24:** 024, **Waypoint 599:** 599

#### DEST Point Reservations
Specific DEST points have specific roles, as seen in the table below.

| Points    | Primary Use         | Planning Programmable | Add/Change in Aircraft           |
|-----------|---------------------|----------------------|----------------------------------|
| 000       | EGI Start Point     | No                   | Yes, only if EGI OFF             |
| 001-350   | Flight Plans 1      | Yes                  | Yes                              |
| 351-399   | User Defined        | Yes                  | Yes                              |
| 400-499   | User Defined        | Yes                  | No                               |
| 500-599   | PPA (TODO WHAT IS THIS) | Yes              | No                               |
| 600-604   | A/G Targets         | No                   | Yes                              |
| 605-610   | Mark Points         | No                   | Yes (using MRK)                  |
| 611-649   | Future Growth       | No                   | No                               |
| 650-999   | Flight Plans 2      | Yes                  | Yes                              |
///caption
DEST point reservations
///

!!! Warning
    Waypoints 611-649 are not editiable, and are skipped in the database all together.

#### Editing DEST Points
DEST Points are editable on the UFCP by pressing the DST Key, and support Lat Long Decimal Minutes Seconds (DMS) or UTM/MGRS format (Not currently implemented). The list of waypoints can be viewed on the DEST page of the MFD, from Menu 1.

!!! Warning
    This is a quick summary, full instructions to come later (TODO)

1. Click **DST** on the UFCP.
2. Select the waypoint you want to edit (e.g., waypoint 10 is entered as 010).
3. Enter coordinates in Lat/Long DMS by pressing the left button of the relevant UFCP row.
4. Swap E/W or N/S by pressing the right button of the relevant row.
5. Enter altitude in the lower left.

---
### Flight Plans
The T-38C supports 20 flight plans, labelled 0-19. These flight plans can be viewed on the FPL page by switching to MENU1 on the MFD, then pressing ML4 on the MFD.

#### FPL MFD Page

ML2 and ML3 allow you to scroll up and down 10 waypoints, ML4 and ML6 move the selection arrow up and down by 1. ML5 selects the current flight plan, and current point of the flight plan to be the current EGI destination.
MB5 and MB6 allow switching between viewed flight plans, this is reflected by the heading box below the ADI showing the name and number
MB2 swaps the FPL page from COORD to ID mode. The default mode is COORD, although ID mode is more commonly used.

!!! Note
    The FPL page on the MFD can also be accessed by pressing the F key on the UFCP anytime text entry is not selected.

---

## VOR

---

## TACAN

---
