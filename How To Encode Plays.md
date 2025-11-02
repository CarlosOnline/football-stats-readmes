# Encoding Plays Instructions
How to encode plays.

## Contents

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Encoding Plays Instructions](#encoding-plays-instructions)
  - [Contents](#contents)
- [Offense](#offense)
      - [Run Play](#run-play)
      - [Pass Play](#pass-play)
      - [QB sacked](#qb-sacked)
- [Defense](#defense)
      - [Run Play](#run-play-1)
      - [Pass Play](#pass-play-1)
        - [Completed pass](#completed-pass)
        - [Incomplete pass](#incomplete-pass)
        - [Interception pass](#interception-pass)
- [Turnover](#turnover)
    - [Turnover](#turnover-1)
        - [Example: Opponent Fumble with optional return yards](#example-opponent-fumble-with-optional-return-yards)
        - [Example: Defense Interception with optional return yards](#example-defense-interception-with-optional-return-yards)
    - [Turnover With Return Yards](#turnover-with-return-yards)
        - [Example: Second play for fumble with return yards](#example-second-play-for-fumble-with-return-yards)
        - [Example: Defense Interception with return yards](#example-defense-interception-with-return-yards)
- [Turnover with Opponent Return Yards](#turnover-with-opponent-return-yards)
        - [Example: Offense fumble](#example-offense-fumble)
- [Penalty](#penalty)
        - [Example: Replay of down due to penalty](#example-replay-of-down-due-to-penalty)
        - [Example: Penalty assesed after play.](#example-penalty-assesed-after-play)

<!-- /code_chunk_output -->



# Offense
Offensive plays

#### Run Play
| Field          | Value        |
| -------------- | ------------ |
| Yard Line      | Scrimmage YL |
| Possession     | LW           |
| Team Unit      | Offense      |
| Play Type      | Run          |
| Jersey numbers | Runner       |


#### Pass Play
- Fill in intended receiver for incomplete / interception.
- For interception fill out below and see [Turnover](#turnover )


| Field          | Value         |
| -------------- | ------------- |
| Yard Line      | Scrimmage YL  |
| Possession     | LW            |
| Team Unit      | Offense       |
| Play Type      | Pass          |
| Pass Outcome   | Complete,etc. |
| Jersey numbers | QB & Receiver |

#### QB sacked

| Field          | Value        |
| -------------- | ------------ |
| Yard Line      | Scrimmage YL |
| Possession     | LW           |
| Team Unit      | Offense      |
| Play Type      | PasS         |
| Pass Outcome   | Sack         |
| Jersey numbers | QB           |


# Defense
Defensive plays

#### Run Play
| Field          | Value         |
| -------------- | ------------- |
| Yard Line      | Scrimmage YL  |
| Possession     | Opponent      |
| Team Unit      | Defense       |
| Play Type      | Run           |
| Jersey numbers | Tackers 1,2,3 |


#### Pass Play

##### Completed pass

| Field          | Value         |
| -------------- | ------------- |
| Yard Line      | Scrimmage YL  |
| Possession     | Opponent      |
| Team Unit      | Defense       |
| Play Type      | Pass          |
| Pass Outcome   | Complete      |
| Jersey numbers | Tackers 1,2,3 |

##### Incomplete pass
Fill in jeresy number of player that defended the pass.

| Field          | Value         |
| -------------- | ------------- |
| Yard Line      | Scrimmage YL  |
| Possession     | Opponent      |
| Team Unit      | Defense       |
| Play Type      | Pass          |
| Pass Outcome   | Incomplete    |
| Jersey numbers | Defender      |

##### Interception pass
Fill in jeresy number of player that defended the pass.

| Field          | Value                          |
| -------------- | ------------------------------ |
| Yard Line      | Scrimmage YL                   |
| Possession     | Opponent                       |
| Team Unit      | Defense                        |
| Play Type      | Pass                           |
| Pass Outcome   | Interception                   |
| Jersey numbers | Interceptor, TD Returner if TD |
| Return Yard    | # of yards                     |

---
# Turnover
Turnover occurs when one of the following happen:
- Interception 
- Fumble
- Blocked Field Goal, 2-Pt attempt

There are two ways to encode turn overs
- Single play if turnover with no return yards
- Dual plays if turnover with return yards

### Turnover

##### Example: Opponent Fumble with optional return yards
While on Defense LW forces and recovers and with optional return yards.
If return yards see [Turnover With Return Yards](#turnover-with-return-yards)


| Field          | Value                               |
| -------------- | ----------------------------------- |
| Yard Line      | Scrimmage YL                        |
| Possession     | Opponent                            |
| Team Unit      | Defense                             |
| Play Type      | Run                                 |
| Fumble         | Turned On                           |
| Fumble Type    | Lost                                |
| Jersey numbers | Forcer,Recoverer, TD Returner if TD |
| Return Yards   | # of yards if any                   |

##### Example: Defense Interception with optional return yards
While on Defense LW intercepts pass and with optional return yards.
If return yards see [Turnover With Return Yards](#turnover-with-return-yards)

| Field          | Value                          |
| -------------- | ------------------------------ |
| Yard Line      | Scrimmage YL                   |
| Possession     | Opponent                       |
| Team Unit      | Defense                        |
| Play Type      | Pass                           |
| Pass Outcome   | Interception                   |
| Jersey numbers | Interceptor, TD Returner if TD |
| Return Yards   | # of yards if any              |

### Turnover With Return Yards
Turnover with return yards are encoded in 2 plays.
- **First play** encodes entire play as above.
- **Second play** encodes just the Turnover YL

Use **Insert Play** button with **Reset** button to add additional play.

##### Example: Second play for fumble with return yards
While on Defense LW forces and recovers a fumble and runs it back some yards.

**Second Play**
| Field      | Value                   |
| ---------- | ----------------------- |
| Yard Line  | Turnover YL             |
| Down       | **NA**                  |
| Possession | LW                      |
| Team Unit  | None                    |
| Play Type  | None                    |
| Play Notes | Turnover YL yardage row |

##### Example: Defense Interception with return yards
While on Defense LW intercepts ball runs it back some yards.

**Second Play**
| Field      | Value                   |
| ---------- | ----------------------- |
| Yard Line  | Turnover YL             |
| Down       | **NA**                  |
| Possession | LW                      |
| Team Unit  | None                    |
| Play Type  | None                    |
| Play Notes | Turnover YL yardage row |

---
# Turnover with Opponent Return Yards
Special case where where the Opponent takes possession and returns the ball.

Encode the play in two rows:
- **First play** encodes the LW Offensive play
- **Second play** encodes the Opponent return

**First Play**

| Field          | Value         |
| -------------- | ------------- |
| Yard Line      | Scrimmage YL  |
| Possession     | LW            |
| Team Unit      | Offense       |
| Play Type      | Pass          |
| Pass Outcome   | Interception  |
| Jersey numbers | QB & Receiver |

**Second Play**
| Field          | Value                                 |
| -------------- | ------------------------------------- |
| Yard Line      | Turnover YL                           |
| Down           | **NA**                                |
| Possession     | Opponent                              |
| Team Unit      | Defense                               |
| Play Type      | Opp Turnover                          |
| Jersey numbers | Tackers 1,2,3                         |
| Play Notes     | Opp intercepted at YL, returned to YL |

##### Example: Offense fumble
While on Offense fumbles and loses possession with optional return yards.
If Opponent return yards see [Turnover With Return Yards](#turnover-with-return-yards)

| Field          | Value            |
| -------------- | ---------------- |
| Yard Line      | Scrimmage YL     |
| Possession     | LW               |
| Team Unit      | Offense          |
| Play Type      | Run              |
| Fumble         | Turned On        |
| Fumble Type    | Lost             |
| Jersey numbers | Runner           |

---
# Penalty
There are 2 types of penalties to record
- Penalty that causes a replay of down, nothing else is tracked from play.
- Penalty that is asseses after play results.

There are two ways to encode penalties
- Single play if penalty replays the down.
- Dual plays if penalty is assesed after the down.

Use **Insert Play** button with **Reset** button to add additional play.

##### Example: Replay of down due to penalty
While on Offense, LW false start penalty, run or pass is not counted.  Down is replayed.

**Penalty Play**
| Field      | Value                            |
| ---------- | -------------------------------- |
| Yard Line  | Scrimmage YL                     |
| Possession | LW                               |
| Team Unit  | Offense                          |
| Play Type  | Penalty - LW                     |
| Play Notes | False start penalty, replay down |

##### Example: Penalty assesed after play.
While on Offense, LW runs the ball 10 yards.  During the play the Opponent grabs face mask.

**First Play**

| Field          | Value         |
| -------------- | ------------- |
| Yard Line      | Scrimmage YL  |
| Possession     | Opponent      |
| Team Unit      | Defense       |
| Play Type      | Run           |
| Jersey numbers | Tackers 1,2,3 |


**Penalty Play**
| Field      | Value                            |
| ---------- | -------------------------------- |
| Yard Line  | End of run or catch YL           |
| Down       | **NA**                           |
| Possession | LW                               |
| Team Unit  | Offense                          |
| Play Type  | Penalty - Opponent               |
| Play Notes | Face mask penalty                |


# Play Notes
Examples:

1Q - LW 1 Yd TD Run (PAT Good)
2Q - LW 1 Yd TD Run (2-pt attempt failed)
2Q - LW 13 Yd TD Run (PAT Blocked)
3Q - LW 10 Yd Safety on Redmond
3Q - LW 6 Yd FG


# Final Forms
Football Team Form_(Date of Game)_LW vs (Opponent)
Football Individual Form_(Date of Game)_LW vs (Opponent)
Football Tackles Form_(Date of Game)_LW vs (Opponent)
