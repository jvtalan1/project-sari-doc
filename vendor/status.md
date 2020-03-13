# Order Document Status

_Updated March 13, 2020 Victor Javier_

### Current Status

| action         | status     |
| -------------- | ---------- |
|                | new        |
| accepted       | accepted   |
| pick/start     | preparing  |
| pick/end       | delivering |
| print/waiting  | delivering |
| print/start    | delivering |
| print/end      | delivering |
| delivery/start | delivering |
| delivery/end   | received   |

### Proposed Enhanced Status

| action           | status     | state         | Vendor        | My Suki                               |
| ---------------- | ---------- | ------------- | ------------- | ------------------------------------- |
|                  | new        | new           | New           | New                                   |
| `accepted`       | accepted   | accepted      | Accepted      | Accepted                              |
| `pick/start`     | preparing  | picking       | Picking       | Preparing                             |
| `pick/end`       | delivering | done-picking  | Done Picking  | Preparing                             |
| `check/start`    | delivering | checking      | Checking      | Final Checking                        |
| `check/end`      | delivering | done-checking | Done Checking | Ready for Delivery / Ready for Pickup |
| `print/waiting`  | delivering |               |               |                                       |
| `print/start`    | delivering |               |               |                                       |
| `print/end`      | delivering |               |               |                                       |
| `delivery/start` | delivering | deliverying   | Delivering    | Delivering                            |
| `delivery/end`   | received   | received      | Received      | Received                              |

### Proposed Enhanced Status with Abort Actions

| action           | status     | state        |
| ---------------- | ---------- | ------------ |
|                  | new        | new          |
| `pick/abort`     | accepted   | accepted     |
| `check/abort`    | delivering | done-picking |
| `print/abort`    | delivering |              |
| `delivery/abort` | delivering | done-picking |
