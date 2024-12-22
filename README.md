This is a detailed description of the **Webserv** project, which involves creating an HTTP server in **C++ 98**. Here's a structured explanation of the key aspects and requirements:  

---

## **Project Overview**
- **Goal**: Build a non-blocking, resilient HTTP server capable of serving static websites, handling HTTP requests (GET, POST, DELETE), and executing CGI scripts.
- **Features**:
  - Serve HTML documents and associated resources (e.g., images, styles, scripts).
  - Process client uploads.
  - Handle multiple ports and configurations.
  - Support for HTTP/1.1 headers and response codes.
  - Provide default error pages.
  - Stress-tested to ensure reliability.

---

## **Setup & Usage**
1. **Compilation**:
   - Use a `Makefile` to compile the project.  
   - The Makefile must support the following commands:
     - `all`: Build the project.
     - `clean`: Remove object files.
     - `fclean`: Remove all generated files, including the executable.
     - `re`: Rebuild the project from scratch.

2. **Execution**:
   - The server must be executable using:
     ```bash
     ./webserv [configuration file]
     ```
   - If no configuration file is provided, a default configuration path should be used.

3. **Dependencies**:
   - Use only C++ 98 features and standard C++ libraries.  
   - System calls and external functions allowed: `epoll`,  `socket`, `listen`, `accept`, `send`, `recv`, `fork`, etc.  
   - No external libraries (e.g., Boost) are allowed.

---

## **Mandatory Features**
### 1. **HTTP Server Requirements**
- **Non-blocking**: Use `epoll()` to handle all I/O operations.  
- **Methods Supported**:  
  - `GET`: Retrieve resources.  
  - `POST`: Accept and process form data or file uploads.  
  - `DELETE`: Remove specified resources.

- **Static Website Support**:
  - Serve HTML, CSS, JavaScript, and other static files.
  - Directory listing and default file serving (e.g., `index.html`).

- **Error Handling**:
  - Provide accurate HTTP status codes (e.g., 404 for missing resources).  
  - Serve default error pages if custom ones are not defined.

- **Configuration File**:
  - Allow defining:
    - Host and port for each server.
    - Default error pages.
    - Maximum client body size.
    - Routes with specific rules (e.g., HTTP methods allowed, CGI execution, file paths, etc.).

### 2. **CGI Support**
- Execute scripts (e.g., PHP, Python) for dynamic content.
- Handle input/output correctly:
  - Unchunk requests for the CGI.
  - Use EOF as the end of the body when no `Content-Length` is specified.
  - Pass requested files as arguments to the CGI.

### 3. **Multiple Ports**
- The server must listen to multiple ports simultaneously, handling requests for each port independently.

---

## **Bonus Features**
- **Session Management**:
  - Implement cookie handling for user sessions.  

- **Enhanced CGI Support**:
  - Allow handling multiple CGI scripts simultaneously.

---

## **Testing Recommendations**
1. **RFC Reading**:
   - Read the HTTP/1.1 RFC for a thorough understanding of protocol behavior.

2. **Comparison with NGINX**:
   - Test server responses and behavior against **NGINX** to ensure compliance.

3. **Tools**:
   - Use tools like **telnet**, Python, or Golang scripts to test and simulate client requests.

4. **Stress Testing**:
   - Simulate high traffic to ensure the server remains available.

5. **Debugging**:
   - Use basic testers provided with the project or build custom tests to identify issues.

---

## **Key Constraints**
- Do not use `execve` to call another web server.
- No direct read/write operations without using `poll()` (or equivalents).
- MacOS-specific: Use `fcntl` only for setting file descriptors to non-blocking mode.

---

This project is a great opportunity to understand how HTTP servers work, including how to manage configurations, handle client requests, and ensure robustness in a real-world application. Let me know if you'd like help with specific parts!
