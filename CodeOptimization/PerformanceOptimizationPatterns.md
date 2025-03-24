# Performance Optimization Patterns with GitHub Copilot

## Prompt 1: Implementing Performance Optimizations
```markdown
Intent: To help developers implement performance optimizations using GitHub Copilot.

Context: Guide the implementation of performance improvements:
- Algorithm optimization
- Resource management
- Caching strategies
- Load handling
```

### Optimization Patterns

1. **Algorithmic Optimization**
```typescript
/**
 * Optimize algorithm for:
 * Task: Data processing pipeline
 * Current complexity: O(n²)
 * Target complexity: O(n log n)
 * Constraints:
 * - Memory usage
 * - Data consistency
 * - Error handling
 */
class DataProcessor {
    process_data_batch(items: DataItem[]): ProcessedResult[] {
        // Copilot will suggest optimized implementation
    }
}
```

2. **Resource Management**
```typescript
/**
 * Implement efficient resource handling:
 * - Memory pooling
 * - Connection management
 * - Batch processing
 * - Resource cleanup
 */
class ResourceManager {
    private resource_pool: Map<string, Resource>;
    
    async acquire_resource<T extends Resource>(
        resource_type: string,
        options: {
            max_pool_size: number;
            idle_timeout_ms: number;
            validation_fn: (resource: T) => boolean;
        }
    ): Promise<T> {
        // Copilot will suggest efficient implementation
    }
}
```

### Performance Patterns

1. **Caching Strategy**
```typescript
/**
 * Implement multi-level caching:
 * - Memory cache
 * - Distributed cache
 * - Cache invalidation
 * - Cache warming
 */
class CacheManager {
    private memory_cache: Map<string, CacheEntry>;
    private distributed_cache: DistributedCache;
    
    async get_or_compute<T>(
        key: string,
        computer: () => Promise<T>,
        options: CacheOptions
    ): Promise<T> {
        // Copilot will suggest efficient caching implementation
    }
}
```

2. **Load Handling**
```typescript
/**
 * Implement load management:
 * - Rate limiting
 * - Circuit breaking
 * - Load shedding
 * - Back pressure
 */
class LoadManager {
    async handle_request<T>(
        request: () => Promise<T>,
        options: {
            max_concurrent: number;
            timeout_ms: number;
            retry_strategy: RetryStrategy;
        }
    ): Promise<T> {
        // Copilot will suggest efficient load handling
    }
}
```

### Data Structure Optimization

1. **Collection Optimization**
```typescript
/**
 * Optimize data structures for:
 * - Fast access patterns
 * - Memory efficiency
 * - Concurrent operations
 * - Bulk operations
 */
class OptimizedCollection<T> {
    private data: Map<string, T>;
    private indexes: Map<string, Map<any, Set<string>>>;
    
    bulk_insert(items: T[]): void {
        // Copilot will suggest efficient implementation
    }
}
```

2. **Memory Management**
```typescript
/**
 * Implement memory-efficient handling:
 * - Object pooling
 * - Lazy loading
 * - Reference management
 * - Garbage collection hints
 */
class MemoryOptimizer {
    private object_pool: Map<string, any[]>;
    
    acquire_from_pool<T>(
        pool_key: string,
        factory: () => T,
        options: PoolOptions
    ): T {
        // Copilot will suggest efficient implementation
    }
}
```

### Query Optimization

1. **Database Queries**
```typescript
/**
 * Optimize database operations:
 * - Query planning
 * - Index usage
 * - Join optimization
 * - Batch operations
 */
class QueryOptimizer {
    optimize_query(
        query: DatabaseQuery,
        context: QueryContext
    ): OptimizedQuery {
        // Copilot will suggest optimizations
    }
}
```

2. **Data Access Patterns**
```typescript
/**
 * Implement efficient data access:
 * - Eager loading
 * - Pagination
 * - Streaming
 * - Partial loading
 */
class DataAccessManager {
    async fetch_data<T>(
        query: DataQuery,
        options: {
            page_size: number;
            eager_load: string[];
            stream_threshold: number;
        }
    ): Promise<DataResult<T>> {
        // Copilot will suggest efficient implementation
    }
}
```

### Performance Monitoring

1. **Metrics Collection**
```typescript
/**
 * Implement performance monitoring:
 * - Response times
 * - Resource usage
 * - Error rates
 * - System health
 */
class PerformanceMonitor {
    private metrics: Map<string, Metric>;
    
    track_operation<T>(
        operation_name: string,
        operation: () => Promise<T>,
        thresholds: MetricThresholds
    ): Promise<T> {
        // Copilot will suggest implementation
    }
}
```

2. **Performance Analysis**
```typescript
/**
 * Analyze performance data:
 * - Trend analysis
 * - Bottleneck detection
 * - Anomaly detection
 * - Capacity planning
 */
class PerformanceAnalyzer {
    analyze_metrics(
        metrics: MetricData[],
        options: AnalysisOptions
    ): PerformanceReport {
        // Copilot will suggest implementation
    }
}
```

### Best Practices

1. **Code Organization**
```typescript
/**
 * Structure code for performance:
 * - Modular design
 * - Efficient imports
 * - Code splitting
 * - Tree shaking
 */
class ModuleManager {
    optimize_imports(
        module_config: ModuleConfig
    ): OptimizedModules {
        // Copilot will suggest implementation
    }
}
```

2. **Runtime Optimization**
```typescript
/**
 * Optimize runtime behavior:
 * - Async operations
 * - Worker threads
 * - Memory management
 * - Event loop optimization
 */
class RuntimeOptimizer {
    optimize_execution(
        task: AsyncTask,
        resources: SystemResources
    ): OptimizedTask {
        // Copilot will suggest implementation
    }
}
```

### Anti-patterns to Avoid

1. **Performance Issues**
   - Premature optimization
   - Memory leaks
   - N+1 queries
   - Blocking operations

2. **Resource Management**
   - Unclosed resources
   - Thread pool abuse
   - Connection leaks
   - Unbounded caches

### Testing Performance

1. **Load Testing**
```typescript
/**
 * Implement performance tests:
 * - Load scenarios
 * - Stress testing
 * - Endurance testing
 * - Capacity testing
 */
class PerformanceTest {
    async run_load_test(
        scenario: TestScenario,
        options: LoadTestOptions
    ): Promise<TestResults> {
        // Copilot will suggest implementation
    }
}
```

2. **Benchmarking**
```typescript
/**
 * Implement benchmarking:
 * - Operation timing
 * - Resource usage
 * - Comparative analysis
 * - Regression testing
 */
class Benchmarker {
    run_benchmark(
        test_case: BenchmarkCase,
        options: BenchmarkOptions
    ): BenchmarkResults {
        // Copilot will suggest implementation
    }
}
```