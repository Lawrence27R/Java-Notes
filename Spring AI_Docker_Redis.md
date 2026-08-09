**Spring AI:**

Spring AI is Spring's official framework for wiring LLMs (OpenAI, Anthropic, Azure OpenAI, Google Vertex, or local models via Ollama) into a Spring Boot application, acting as an abstraction layer that lets you plug in LLMs without hardcoding a specific AI provider. The pitch is the same one Spring has always made: instead of writing raw HTTP calls to an AI vendor's API, you get familiar Spring patterns — auto-configuration, dependency injection, starters — so you write ordinary Spring code and Spring AI handles the underlying API plumbing. 

Medium

JOptimize



How it works — the core pieces



ChatModel — a portable interface. Your code talks to this interface, not to "OpenAI" or "Anthropic" directly. Swapping the underlying provider is mostly a configuration change — no rewritten business logic. 

Form.io

ChatClient — the main API you actually call day to day. It's a fluent API for talking to chat models, deliberately similar in style to Spring's WebClient/RestClient — so it'll feel immediately familiar to you. 



RAG (Retrieval-Augmented Generation) — the piece that actually matters for an FAQ use case. Instead of asking a general-purpose LLM a question and hoping it "knows" your company's policies, you first do a similarity search against a VectorStore containing your own documents, then hand the LLM only the relevant chunks along with the question. Spring AI does this by attaching a QuestionAnswerAdvisor built from a vector store to the ChatClient; the advisor runs a similarity search over the documents before the question ever reaches the model



Customer question (Angular chat widget)

&#x20;     │

&#x20;     ▼

REST endpoint (Spring Boot Controller)

&#x20;     │

&#x20;     ▼

ChatClient.prompt()

&#x20;     │

&#x20;     ├── QuestionAnswerAdvisor → similarity search against VectorStore

&#x20;     │       (VectorStore = embeddings of your FAQ docs, T\&Cs, 

&#x20;     │        transaction-timing policies, etc.)

&#x20;     │

&#x20;     ├── MessageChatMemoryAdvisor → remembers earlier turns in the chat

&#x20;     │

&#x20;     ▼

LLM generates answer grounded ONLY in retrieved bank documents

&#x20;     │

&#x20;     ▼

Response streamed back to Angular frontend



Approach 1: Build it from existing FAQ Q\&A pairs (retrieval-based, no training)



This is what Spring AI's RAG setup does — and it's the one I'd recommend for a banking FAQ.



You take your existing FAQ content (question + answer pairs, policy docs, T\&Cs) and convert each into a vector embedding, stored in a VectorStore.

When a customer asks something, you embed their question, do a similarity search to find the closest matching FAQ entries, and hand those to the LLM as context.

The LLM's job is just to phrase a natural answer using that retrieved content — it's not "deciding" facts from its own training, it's summarizing what you gave it.



No model training involved. You're just indexing your existing content. This is fast to set up, easy to update (add a new FAQ entry → re-embed it, done — no retraining), and — critically for banking — auditable: you can always trace an answer back to which document it came from.



Approach 2: Fine-tuning / training a model on your data



This means actually adjusting the model's weights using your Q\&A data as training examples, so the model "internalizes" your bank's policies rather than looking them up each time.



Much more expensive and slower to iterate — every policy update means retraining.

Higher hallucination risk — a fine-tuned model can still blend its training data with the general knowledge it already had, and confidently state something wrong.

Much harder to audit — you can't point to "this exact document" as the source of an answer the way you can with RAG.

Generally not recommended for something like transaction timing rules or fee policies that change and where wrong answers have real compliance/customer-trust consequences.



Why RAG wins for a banking FAQ specifically



If a customer asks "what's my NEFT cutoff time" and the bank changes that cutoff next month, with RAG you just update the source document and the next query picks it up immediately. With fine-tuning, the model would keep confidently giving the old answer until you retrain — a real compliance risk in a regulated environment.



**Redis:**

If you mean Redis, it’s an in-memory data store commonly used for caching, sessions, queues, rate limiting, and fast temporary data.



User

&#x20; ↓

Backend API

&#x20; ↓

Redis  ←── fast cache

&#x20; ↓

Database (MySQL/PostgreSQL/etc.)



Caching	Store frequently requested product/user data

Session storage	Login sessions for web applications

Rate limiting	Allow only 100 API requests/minute



Redis primarily stores data in memory (RAM), which makes reads/writes extremely fast.

A Redis server normally has a configuration file called:

redis.conf

\# Port

port 6379



\# Listen address

bind 127.0.0.1



\# Require authentication

requirepass yourStrongPassword



\# Maximum memory

maxmemory 512mb



\# What to do when memory is full

maxmemory-policy allkeys-lru





Docker:

Docker is a containerization platform. It packages an application along with its dependencies and configuration into a container, so the application can run consistently across different environments.

The important Docker concepts are:



Dockerfile → instructions for building your application image

Image → packaged application

Container → running instance of an image

Docker Compose → run multiple containers together

Registry → place where images are stored, e.g. Docker Hub/private registry



FROM eclipse-temurin:21-jre



WORKDIR /app



COPY target/my-app.jar app.jar



EXPOSE 8080



ENTRYPOINT \["java", "-jar", "app.jar"]



Create a Dockerfile

Define how to build the application image.



Build the Docker image



docker build -t myapp:1.0 .



Run the container



docker run -d -p 8080:8080 myapp:1.0



Push the image to a Docker registry

For example, Docker Hub or a private company registry.



docker push myapp:1.0



Deploy on the server

Pull the image and run it:



docker pull myapp:1.0

docker run -d -p 8080:8080 myapp:1.0



JUnit:

JUnit is a testing framework for Java. It is used to write and run unit tests to verify that individual methods or pieces of code work correctly.

1\. Add JUnit dependency



In a Spring Boot project, JUnit usually comes with:

2\. Create a test class

@Test - overmethod

JUnit together with Mockito.

Mock Service and Repository

@Mock

@InjectMock

execute the method I want to test, and use assertions such as assertEquals, assertTrue, and assertNotNull to verify the result.



Linux:



| Command  | Used for                               |

| -------- | -------------------------------------- |

| `pwd`    | Shows the current directory            |

| `ls`     | Lists files and directories            |

| `ls -la` | Lists all files including hidden files |

| `cd`     | Changes the current directory          |

| `mkdir`  | Creates a directory                    |

| `rmdir`  | Removes an empty directory             |

| `touch`  | Creates a new empty file               |

| `cp`     | Copies files or directories            |

| `mv`     | Moves or renames files/directories     |

| `rm`     | Removes a file                         |

| `rm -rf` | Removes a directory and its contents   |

| `find`   | Searches for files/directories         |

| Command   | Used for                              |

| --------- | ------------------------------------- |

| `cat`     | Displays file contents                |

| `less`    | Views a file page by page             |

| `head`    | Shows the beginning of a file         |

| `tail`    | Shows the end of a file               |

| `tail -f` | Continuously monitors new log entries |

| `grep`    | Searches for text/patterns            |

| `grep -i` | Searches text ignoring case           |

| `wc`      | Counts lines, words, or characters    |

| Command    | Used for                         |

| ---------- | -------------------------------- |

| `ps`       | Shows running processes          |

| `ps aux`   | Shows detailed running processes |

| `top`      | Monitors CPU and memory usage    |

| `kill`     | Stops a running process          |

| `kill -9`  | Forcefully stops a process       |

| `df -h`    | Shows disk space usage           |

| `du -sh`   | Shows directory/file size        |

| `free -h`  | Shows memory usage               |

| `uname -a` | Shows system information         |

| Command    | Used for                                      |

| ---------- | --------------------------------------------- |

| `ping`     | Checks network connectivity                   |

| `curl`     | Sends HTTP requests / tests APIs              |

| `ss`       | Shows network connections and listening ports |

| `ip addr`  | Shows network/IP addresses                    |

| `nslookup` | Checks DNS information                        |

| Command  | Used for                                    |

| -------- | ------------------------------------------- |

| `chmod`  | Changes file/directory permissions          |

| `chown`  | Changes file/directory ownership            |

| `sudo`   | Executes a command with elevated privileges |

| `whoami` | Shows the current user                      |

| `id`     | Shows user and group information            |

| Command      | Used for                          |

| ------------ | --------------------------------- |

| `ssh`        | Connects to a remote Linux server |

| `scp`        | Copies files between machines     |

| `systemctl`  | Manages Linux services            |

| `journalctl` | Views system/service logs         |

| `env`        | Shows environment variables       |

| `export`     | Sets an environment variable      |

| Command               | Used for                              |

| --------------------- | ------------------------------------- |

| `docker ps`           | Shows running containers              |

| `docker ps -a`        | Shows all containers                  |

| `docker images`       | Lists Docker images                   |

| `docker build`        | Builds a Docker image                 |

| `docker run`          | Creates and starts a container        |

| `docker start`        | Starts a stopped container            |

| `docker stop`         | Stops a running container             |

| `docker restart`      | Restarts a container                  |

| `docker rm`           | Removes a container                   |

| `docker rmi`          | Removes a Docker image                |

| `docker logs`         | Shows container logs                  |

| `docker exec`         | Executes a command inside a container |

| `docker pull`         | Downloads an image from a registry    |

| `docker push`         | Uploads an image to a registry        |

| `docker compose up`   | Starts services defined in Compose    |

| `docker compose down` | Stops and removes Compose services    |

| `docker compose logs` | Shows Compose service logs            |





