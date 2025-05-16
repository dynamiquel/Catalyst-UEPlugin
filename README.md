## Catalyst for Unreal Engine
[Catalyst](https://github.com/dynamiquel/Catalyst) is an opinionated API development tool and Interface Definition Language (IDL) designed to simplify the process of building and consuming APIs across multiple programming languages. It aims to alleviate the pain points of repetitive code writing and the complexities of integrating disparate technologies.

This repository is an Unreal Engine 5 plugin that makes it easier to integrate Catalyst into your own Unreal Engine projects.
Usually, Catalyst tries to avoid adding too many dependencies but Unreal Engine lacks many useful features out-of-the-box.

### Example
```cpp
TSharedRef<Catalyst::Example::FQueryRoles> QueryRolesOp = Client->QueryRoles(FCatalystExampleQueryRolesRequest());
QueryRolesOp->Then([this](TSharedRef<Catalyst::Example::FQueryRoles> Operation)
{
    TSharedPtr<FCatalystExampleQueryRolesResponse> Response = Operation->GetResponse();
    if (!Response.IsValid())
    {
        TSharedPtr<IHttpResponse> Error = Operation->GetError();
      
        UE_LOG(LogTemp, Error, TEXT("Received an invalid response from Query Users"));
        UE_LOG(LogTemp, Error, TEXT("Code: %d - Str: %s"), Error->GetResponseCode(), *Error->GetContentAsString());
        return;
    }
    else
    {
        UE_LOG(LogTemp, Log, TEXT("Received a valid response from Query Users"));
    }
}
```
You can view more examples [here](Source/Catalyst/Private/Example)
