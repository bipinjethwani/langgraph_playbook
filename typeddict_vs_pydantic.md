**TypedDict** (from `typing`) and **Pydantic models** serve different purposes:

| Aspect | TypedDict | Pydantic Model |
|--------|-----------|----------------|
| **Runtime validation** | None - only static type hints | Full validation at runtime |
| **Data coercion** | No | Yes (e.g., `"123"` → `123`) |
| **Default values** | Not supported | Supported |
| **Methods/properties** | Not allowed | Fully supported |
| **Serialization** | Manual | Built-in `.model_dump()`, `.model_dump_json()` |
| **Performance** | Faster (just a dict) | Slower (validation overhead) |
| **Instance type** | Plain `dict` | Pydantic model object |

**TypedDict example:**
```python
from typing import TypedDict

class User(TypedDict):
    name: str
    age: int

user: User = {"name": "Alice", "age": 30}  # Just a dict, no validation
```

**Pydantic example:**
```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int = 0  # default supported

user = User(name="Alice", age="30")  # validates & coerces "30" → 30
```

**When to use:**
- **TypedDict**: When you need type hints for dicts without runtime overhead (e.g., JSON responses you trust)
- **Pydantic**: When you need validation, serialization, or working with untrusted/external data

---

**See also:** [Pydantic Notebook](notebooks/pydantic01.ipynb)
