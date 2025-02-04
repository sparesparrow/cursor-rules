---
description: Resource management rules and guidelines for Model Context Protocol
globs: ["src/mcp/**/resources/**/*.ts"]
---

# MCP Resource Management Rules

## Resource Definition

### Resource Interface
```typescript
interface Resource {
  uri: string;           // Unique resource identifier
  name: string;          // Human-readable name
  description?: string;  // Optional description
  mimeType?: string;    // Content type
  metadata?: Record<string, unknown>; // Additional metadata
}

interface ResourceContent {
  uri: string;
  mimeType?: string;
  content: string | Uint8Array | object;
  encoding?: string;
}
```

### URI Structure Guidelines

1. **Pattern**: `scheme://category/type/identifier`
   ```typescript
   // Examples
   const validUris = [
     "podman://containers/list",
     "file://workspace/src/main.ts",
     "http://api.example.com/data/users"
   ];
   ```

2. **Validation Rules**
   ```typescript
   class UriValidator {
     static validate(uri: string): boolean {
       const pattern = /^[a-z]+:\/\/[a-z0-9-]+(?:\/[a-z0-9-]+)*$/i;
       return pattern.test(uri);
     }
     
     static parse(uri: string): {
       scheme: string;
       category: string;
       type: string;
       identifier?: string;
     } {
       // Implementation
     }
   }
   ```

## Resource Handler Implementation

### Basic Handler
```typescript
class ResourceHandler {
  async readResource(uri: string): Promise<ResourceContent> {
    try {
      const resource = await this.resolveResource(uri);
      return await this.fetchContent(resource);
    } catch (error) {
      throw new MCPError(
        MCPErrorCode.ResourceError,
        `Failed to read resource: ${error.message}`
      );
    }
  }

  async writeResource(
    uri: string,
    content: ResourceContent
  ): Promise<void> {
    try {
      await this.validateContent(content);
      await this.storeContent(uri, content);
    } catch (error) {
      throw new MCPError(
        MCPErrorCode.ResourceError,
        `Failed to write resource: ${error.message}`
      );
    }
  }
}
```

### Streaming Support
```typescript
interface ResourceStream {
  start(): Promise<void>;
  stop(): Promise<void>;
  onData(callback: (content: ResourceContent) => void): void;
  onError(callback: (error: Error) => void): void;
}

class ResourceStreamer {
  createStream(uri: string, options?: {
    interval?: number;
    filter?: (content: ResourceContent) => boolean;
  }): ResourceStream {
    // Implementation
  }
}
```

## Caching Strategy

### Cache Implementation
```typescript
interface CacheOptions {
  ttl: number;
  maxSize: number;
  validateOnGet?: boolean;
}

class ResourceCache {
  constructor(private options: CacheOptions) {}

  async get(uri: string): Promise<ResourceContent | null> {
    const entry = await this.getCacheEntry(uri);
    if (!entry) return null;
    
    if (this.isExpired(entry)) {
      await this.invalidate(uri);
      return null;
    }
    
    return entry.content;
  }

  async set(uri: string, content: ResourceContent): Promise<void> {
    await this.evictIfNeeded();
    await this.setCacheEntry(uri, content);
  }
}
```

## Resource Lifecycle Management

### Lifecycle States
```typescript
enum ResourceState {
  Created = 'created',
  Available = 'available',
  Locked = 'locked',
  Deleted = 'deleted'
}

class ResourceLifecycle {
  async transition(
    uri: string,
    targetState: ResourceState
  ): Promise<void> {
    const currentState = await this.getState(uri);
    if (!this.isValidTransition(currentState, targetState)) {
      throw new Error(`Invalid state transition: ${currentState} -> ${targetState}`);
    }
    await this.updateState(uri, targetState);
  }
}
```

## Best Practices

1. **Resource Resolution**
   - Implement proper URI validation
   - Handle missing resources gracefully
   - Support resource discovery

2. **Content Handling**
   - Validate content types
   - Support content transformation
   - Implement proper encoding

3. **Error Handling**
   - Use specific error types
   - Include context in errors
   - Handle cleanup on errors

4. **Performance**
   - Implement efficient caching
   - Use streaming for large resources
   - Support batch operations

## Implementation Guidelines

1. **Resource Creation**
   ```typescript
   async function createResource(
     definition: Resource
   ): Promise<Resource> {
     await validateDefinition(definition);
     await ensureUniqueUri(definition.uri);
     return await storeResource(definition);
   }
   ```

2. **Resource Access**
   ```typescript
   async function accessResource(
     uri: string,
     options: AccessOptions
   ): Promise<ResourceContent> {
     await validateAccess(uri, options);
     return await fetchResourceContent(uri);
   }
   ```

3. **Resource Cleanup**
   ```typescript
   async function cleanupResource(
     uri: string
   ): Promise<void> {
     await invalidateCache(uri);
     await removeContent(uri);
     await updateRegistry(uri);
   }
   ``` 