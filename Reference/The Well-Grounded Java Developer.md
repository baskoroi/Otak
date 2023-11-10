#reference-book #java #tech 

## Chapter 1 - Introducing Modern Java
### "Java Language" vs "Java Platform"
**What's the difference?**
- Java _language_ = the programming language, the set of constructs & grammars/syntax that govern how Java must be written
- Java _platform_ = the software providing the runtime environment that processes Java source code -> class files -> linked binaries/executable

One reason Java as a software system (i.e. Java platform) is successful => 'cuz **Java is a standard**.
- Java is standardized by specifications -> most notably the JLS (Java Language Specification) and VMSpec (Java Virtual Machine Specification)
	- Different projects / vendors can implement JVM versions with different characteristics, and yet still play by the same rules governed by those specs.
		- Thus despite the differences, the correctness of the JVM operations is still guaranteed.
		- JVM is *actually* a general-purpose and language-agnostic runtime env, hence the separation of those specs.

Is Java a compiled/interpreted language? **Both.** See how a Java app works in below diagram:

![[Pasted image 20231029123536.png]]
- "Executing code" = JVM bytecode (IL / intermediate language)
	- bytecode is basically half code half executable -> which can be compiled by JIT compiler into executable/binary~! yaay...

### Java release model

Java started open-sourcing their source code at Java 7, under the GPLv2+CE license -> under the [OpenJDK project](https://openjdk.org).
- Their mailing list is rife with creative/explorative projects, some of which can be used as future Java features.

Shortly before Java 7 was released, Oracle bought Sun Microsystems.

Java 7, 8, and 9 were released by a feature-driven release cycle, where a single large feature determines each release.

Starting from Java 10, Oracle decides to release Java by a time-based model, where each major release is released every six months, and each LTS version every three years (now as of this writing: each LTS = two years.)
- New features are developed on a branch and merged only when they are code complete.
- Releases can occur on a strict time cadence.
- Late features do not delay releases but are held over for the next release.
- The current head of the trunk should always be releasable (in theory).
- If necessary, an emergency fix can be prepared and pushed out at any point.
- Separate OpenJDK projects are used to explore and research longer-term, future directions.

![[Pasted image 20231029135733.png]]

Another change at Java 11's JDK by Oracle:
- source code is still OSS from OpenJDK, but Oracle JDK binaries have proprietary license.