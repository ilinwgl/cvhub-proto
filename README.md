# CVHub Proto Repository

This repository contains all Protocol Buffers (.proto) definitions used by the CVHub microservices system. 
It serves as the single source of truth for message formats and gRPC service interfaces across all CVHub services.

## Purpose

- Define all request and response message formats (e.g., ImageRequest, DetectResponse).
- Define all gRPC service interfaces (e.g., OCRService, ObjectDetectionService, SegmentationService).
- Ensure consistent communication between services written in different languages (C++, Python, C#, etc.).
- Enable clients to generate language-specific stubs for cross-language communication.

## Usage

1. Clone this repository.
2. Use `protoc` with the appropriate gRPC plugin to generate client and server stubs in your target language:

```bash
# Example for C++
protoc --grpc_out=. --plugin=protoc-gen-grpc=`which grpc_cpp_plugin` cvhub.proto
protoc --cpp_out=. cvhub.proto

# Example for Python
python -m grpc_tools.protoc -I. --python_out=. --grpc_python_out=. cvhub.proto
```

3. Import the generated files into your microservice or client project.

## Repository Structure
```text
cvhub-proto/
├── cvhub.proto          # Main proto file with all service & message definitions
├── README.md
└── LICENSE
```

## Guidelines
- Always update this repository first before adding new RPC services or messages.
- Increment field numbers in messages carefully to maintain backward compatibility.
- Tag versions when making breaking changes, so microservices can track compatible proto versions.
