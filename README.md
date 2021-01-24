# DLV Program

This DLV-Program guesses and then checks schedules for tasks to be executed within given constraints.

## General
The time in this Program can be represented by a integer.

>*In the Range of (60*24) if a granularity of minutes over one day is needed.* \
>*This can be Scpecified by the argument ```-N=1440```*

The dlv executable is a "dependency" under a different license that must be downloaded from the [dlvsystem-site](http://www.dlvsystem.com/dlv/).

## Day
```
day(dayname)
```
This predicate represents a day

Arguments:
* __dayname__ \
The name of the 'day'

## Slot
```
slot(start,finish,dayname,id).
```
Represents a slot where a task can be executed.

Arguments:
* __start__:\
    The start time of the slot.
* __finish__:\
    The ending time of the slot.
* __dayname__:\
    The name of the day. Musst satisfy the predicate ```day(dayname)```
* __id__:\
    The id identifying the "room" in which the slot is available.

## Task
```
task(start,finish,id).
```
Represents a task that will be executed.

Arguments:
* __start__:\
    The start time of the task.
* __finish__:\
    The ending time of the task.
* __dayname__:\
    The name of the day the task will be executed on. Musst satisfy the predicate ```day(dayname)```
* __id__:\
    The id identifying the "room" in which the task will be executed.


## Room
```
room(count,duration,id).
```
Represents a room on which slots and tasks can be defined and executed respectively.

Arguments:
* __count__:\
    The number of tasks to be executed on this room in total.
* __duration__:\
    The duration to execute a task on this room
* __id__:\
    The id identifying this room.

## Tests
Tests are located in the /tests directory and are examples for schedules.
The correctness still has to be checked by hand. Due to the simplicity of the test this should be doable.


## Examples
The program can be called with:

```
./dlv ./tests/timetable_test1.dl ./timetable_guess.dl ./timetable_check.dl -N=1440
```
> Use of the argument -pfilter mentioned later is recomended to minimize the output

This command will call the program on the facts given in *./timetable_test1.dl* and the guess and check in *timetable_guess.dl* and *timetable_check.dl*.
The limit for integers will be 1440. So conceptually ```slot(60,120,mo,1)``` will be a slot starting at 1 AM, ending at 2 AM on the day 'mo' and in the room with id 1.

```
./dlv ./tests/timetable_test1.dl ./timetable_guess.dl ./timetable_check.dl -N=1440 -pfilter=task
```
This command will do the same as the above but will only print the task predicates in the resulting answersets.

## TODO

- [x] :rocket: write some tests
- [x] :bulb: write the guessing part
- [x] :heavy_check_mark: write the checking part
- [ ] :recycle: automate tests
- [ ] :speech_balloon: update README to link definitions
