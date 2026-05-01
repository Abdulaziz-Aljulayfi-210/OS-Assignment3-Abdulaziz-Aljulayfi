# Assignment 3 - Complete Documentation

**Student Name**: [Your Full Name]  
**Student ID**: [Your ID]  
**Date Submitted**: [Submission Date]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [Paste your personal Gmail Google Drive link here]

**Video filename**: `[YourStudentID]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - 1-may
What I implemented: I added ReentrantLock for all shared counters in the SharedResources class.
Challenges encountered: I wasn't sure if I should use one lock for everything or separate locks.
How I solved it: I used separate locks (fine-grained) to allow better performance and less waiting time.
Testing approach: I ran the code and checked if the final counts matched the number of processes.
Time spent: 1h

---

### Entry 2 - 1-may      
What I implemented: Integrated the Semaphore to control CPU access in the Process class.
Challenges encountered: The program was freezing because I forgot to release the semaphore.
How I solved it: I placed the release() method inside a finally block to ensure it always runs.
Testing approach: Observed the console to ensure only one process is "executing" at a time.
Time spent:1h
---

### Entry 3 - 1-may
What I implemented: Synchronized the executionLog and fixed the terminal output.
Challenges encountered: The log list was throwing errors when multiple threads tried to write at once.
How I solved it: I wrapped the executionLog.add() call inside a lock-protected method.
Testing approach: Verified the final log size to ensure no messages were lost.
Time spent:1.5h
---

### Entry 4 - [Date, Time]
**What I implemented**: 

**Challenges encountered**: 

**How I solved it**: 

**Testing approach**: 

**Time spent**: 

---

### Entry 5 - [Date, Time]
**What I implemented**: 

**Challenges encountered**: 

**How I solved it**: 

**Testing approach**: 

**Time spent**: 

---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur?

**Your Answer**:
The original code contains race conditions in shared resources like contextSwitchCount and the executionLog list. For the counters, concurrent access is a problem because multiple threads may read and update the same value simultaneously leading to lost updates where the final total is lower than expected. For the executionLog, simultaneous access to the ArrayList can cause a ConcurrentModificationException or data corruption. By using ReentrantLock, I ensured that only one thread can modify these resources at any given time, maintaining data integrity.

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:
ReentrantLock is a mutual exclusion mechanism (Mutex) designed to protect shared state; I used it for counters and logs to ensure that only one thread enters the critical section. In contrast, a Semaphore manages a set of permits to control access to a resource pool. I used a Semaphore(1) to represent the CPU, which limits the number of processes executing their burst time concurrently. While locks are for "ownership" of data, semaphores are better for "signaling" and limiting concurrent execution in the simulation.

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:
A deadlock occurs when two or more threads are blocked forever, each waiting for a resource held by the other. To prevent this, I used try-finally blocks to guarantee that lock.unlock() and semaphore.release() are always executed, even if the thread is interrupted. Additionally, I followed a resource ordering strategy and kept critical sections extremely short. This ensures that no thread holds a lock longer than necessary, significantly reducing the circular wait condition required for a deadlock to happen.

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:
I implemented fine-grained locking by using separate ReentrantLock objects for each of the three counters (contextSwitchLock, completedProcessLock, and waitingTimeLock). Since these counters are logically independent, this choice allows multiple threads to update different counters simultaneously without blocking each other. A single coarse-grained lock would be simpler but would force a thread updating the "waiting time" to wait for another thread updating "context switches," which decreases performance. Therefore, fine-grained locking provides better concurrency and higher throughput for the simulation.

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 

**Why they need protection**: 

**Synchronization mechanism used**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Justification**: 

---

### Critical Section #2: Execution Log

**What resource**: 

**Why it needs protection**: 

**Synchronization mechanism used**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Justification**: 

---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 

**Number of permits and why**: 

**Where implemented**: 

**Code snippet**:
```java
// Paste your implementation here
```

**Effect on program behavior**: 

---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
```

**Results**: 
(Show that running multiple times produces consistent, correct results)

**Why synchronization is necessary**: 
(Explain what race conditions COULD occur without synchronization, even if you didn't observe them. Explain which shared resources need protection and why.)

**Conclusion**: 

---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 

**Results**: 

**What this proves**: 

---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 

**Actual values**: 

**Analysis**: 

---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]

**Purpose**: 

**Results**: 

**What I learned**: 

---

## Part 5: Reflection and Learning

### What I learned about synchronization:

[6-8 sentences about key concepts, challenges, insights]

---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 

**Example 2**: 

---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]

---

## Part 6: GitHub Repository Information

**Repository URL**: 

**Number of commits**: 

**Commit messages**: 
1. 
2. 
3. 
4. 

---

## Summary

**Total time spent on assignment**: 

**Key takeaways**: 
1. 
2. 
3. 

**Most challenging aspect**: 

**What I'm most proud of**: 

---

**End of Documentation**
