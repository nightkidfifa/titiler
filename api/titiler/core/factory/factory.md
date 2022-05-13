# Module titiler.core.factory

TiTiler Router factories.

None

## Variables

```python3
img_endpoint_params
```

```python3
templates
```

## Classes

### BaseTilerFactory

```python3
class BaseTilerFactory(
    reader: Type[rio_tiler.io.base.BaseReader],
    router: fastapi.routing.APIRouter = <factory>,
    path_dependency: Callable[..., Any] = <function DatasetPathParams at 0x7fe57c81aa60>,
    dataset_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.DatasetParams'>,
    layer_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.BidxExprParams'>,
    render_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.ImageRenderingParams'>,
    colormap_dependency: Callable[..., Union[Dict[int, Tuple[int, int, int, int]], Sequence[Tuple[Tuple[Union[float, int], Union[float, int]], Tuple[int, int, int, int]]], NoneType]] = <function ColorMapParams at 0x7fe57ca0d040>,
    stats_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.StatisticsParams'>,
    histogram_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.HistogramParams'>,
    process_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.PostProcessParams'>,
    tms_dependency: Callable[..., morecantile.models.TileMatrixSet] = <function TMSParams at 0x7fe57f43d700>,
    reader_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.DefaultDependency'>,
    router_prefix: str = '',
    gdal_config: Dict = <factory>,
    optional_headers: List[titiler.core.resources.enums.OptionalHeader] = <factory>,
    route_dependencies: List[Tuple[List[titiler.core.routing.EndpointScope], List[fastapi.params.Depends]]] = <factory>
)
```

#### Attributes

| Name | Type | Description | Default |
|---|---|---|---|
| reader | rio_tiler.io.base.BaseReader | A rio-tiler reader (e.g COGReader). | None |
| router | fastapi.APIRouter | Application router to register endpoints to. | None |
| path_dependency | Callable | Endpoint dependency defining `path` to pass to the reader init. | None |
| dataset_dependency | titiler.core.dependencies.DefaultDependency | Endpoint dependency defining dataset overwriting options (e.g nodata). | None |
| layer_dependency | titiler.core.dependencies.DefaultDependency | Endpoint dependency defining dataset indexes/bands/assets options. | None |
| render_dependency | titiler.core.dependencies.DefaultDependency | Endpoint dependency defining image rendering options (e.g add_mask). | None |
| colormap_dependency | Callable | Endpoint dependency defining ColorMap options (e.g colormap_name). | None |
| stats_dependency | titiler.core.dependencies.DefaultDependency | Endpoint dependency defining options for rio-tiler's statistics method. | None |
| histogram_dependency | titiler.core.dependencies.DefaultDependency | Endpoint dependency defining options for numpy's histogram method. | None |
| process_dependency | titiler.core.dependencies.DefaultDependency | Endpoint dependency defining image post-processing options (e.g rescaling, color-formula). | None |
| tms_dependency | Callable | Endpoint dependency defining TileMatrixSet to use. | None |
| router_prefix | str | prefix where the router will be mounted in the application. | None |
| gdal_config | dict | GDAL environment config to set within endpoint calls. | None |
| optional_headers | sequence of titiler.core.resources.enums.OptionalHeader | additional headers to return with the response. | None |

#### Descendants

* titiler.core.factory.TilerFactory

#### Class variables

```python3
dataset_dependency
```

```python3
histogram_dependency
```

```python3
layer_dependency
```

```python3
process_dependency
```

```python3
reader_dependency
```

```python3
render_dependency
```

```python3
router_prefix
```

```python3
stats_dependency
```

#### Methods

    
#### add_route_dependencies

```python3
def add_route_dependencies(
    self,
    *,
    scopes: List[titiler.core.routing.EndpointScope],
    dependencies=typing.List[fastapi.params.Depends]
)
```

    
Add dependencies to routes.

Allows a developer to add dependencies to a route after the route has been defined.

    
#### colormap_dependency

```python3
def colormap_dependency(
    colormap_name: titiler.core.dependencies.ColorMapName = Query(None),
    colormap: str = Query(None)
) -> Union[Dict[int, Tuple[int, int, int, int]], Sequence[Tuple[Tuple[Union[float, int], Union[float, int]], Tuple[int, int, int, int]]], NoneType]
```

    
Colormap Dependency.

    
#### path_dependency

```python3
def path_dependency(
    url: str = Query(Ellipsis)
) -> str
```

    
Create dataset path from args

    
#### register_routes

```python3
def register_routes(
    self
)
```

    
Register Tiler Routes.

    
#### tms_dependency

```python3
def tms_dependency(
    TileMatrixSetId: titiler.core.dependencies.TileMatrixSetName = Query(TileMatrixSetName.WebMercatorQuad)
) -> morecantile.models.TileMatrixSet
```

    
TileMatrixSet Dependency.

    
#### url_for

```python3
def url_for(
    self,
    request: starlette.requests.Request,
    name: str,
    **path_params: Any
) -> str
```

    
Return full url (with prefix) for a specific endpoint.

### MultiBandTilerFactory

```python3
class MultiBandTilerFactory(
    reader: Type[rio_tiler.io.base.MultiBandReader] = <class 'rio_tiler.io.cogeo.COGReader'>,
    router: fastapi.routing.APIRouter = <factory>,
    path_dependency: Callable[..., Any] = <function DatasetPathParams at 0x7fe57c81aa60>,
    dataset_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.DatasetParams'>,
    layer_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.BandsExprParams'>,
    render_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.ImageRenderingParams'>,
    colormap_dependency: Callable[..., Union[Dict[int, Tuple[int, int, int, int]], Sequence[Tuple[Tuple[Union[float, int], Union[float, int]], Tuple[int, int, int, int]]], NoneType]] = <function ColorMapParams at 0x7fe57ca0d040>,
    stats_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.StatisticsParams'>,
    histogram_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.HistogramParams'>,
    process_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.PostProcessParams'>,
    tms_dependency: Callable[..., morecantile.models.TileMatrixSet] = <function TMSParams at 0x7fe57f43d700>,
    reader_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.DefaultDependency'>,
    router_prefix: str = '',
    gdal_config: Dict = <factory>,
    optional_headers: List[titiler.core.resources.enums.OptionalHeader] = <factory>,
    route_dependencies: List[Tuple[List[titiler.core.routing.EndpointScope], List[fastapi.params.Depends]]] = <factory>,
    img_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.ImageParams'>,
    add_preview: bool = True,
    add_part: bool = True,
    bands_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.BandsParams'>
)
```

#### Ancestors (in MRO)

* titiler.core.factory.TilerFactory
* titiler.core.factory.BaseTilerFactory

#### Class variables

```python3
add_part
```

```python3
add_preview
```

```python3
bands_dependency
```

```python3
dataset_dependency
```

```python3
histogram_dependency
```

```python3
img_dependency
```

```python3
layer_dependency
```

```python3
process_dependency
```

```python3
reader
```

```python3
reader_dependency
```

```python3
render_dependency
```

```python3
router_prefix
```

```python3
stats_dependency
```

#### Methods

    
#### add_route_dependencies

```python3
def add_route_dependencies(
    self,
    *,
    scopes: List[titiler.core.routing.EndpointScope],
    dependencies=typing.List[fastapi.params.Depends]
)
```

    
Add dependencies to routes.

Allows a developer to add dependencies to a route after the route has been defined.

    
#### bounds

```python3
def bounds(
    self
)
```

    
Register /bounds endpoint.

    
#### colormap_dependency

```python3
def colormap_dependency(
    colormap_name: titiler.core.dependencies.ColorMapName = Query(None),
    colormap: str = Query(None)
) -> Union[Dict[int, Tuple[int, int, int, int]], Sequence[Tuple[Tuple[Union[float, int], Union[float, int]], Tuple[int, int, int, int]]], NoneType]
```

    
Colormap Dependency.

    
#### info

```python3
def info(
    self
)
```

    
Register /info endpoint.

    
#### part

```python3
def part(
    self
)
```

    
Register /crop endpoint.

    
#### path_dependency

```python3
def path_dependency(
    url: str = Query(Ellipsis)
) -> str
```

    
Create dataset path from args

    
#### point

```python3
def point(
    self
)
```

    
Register /point endpoints.

    
#### preview

```python3
def preview(
    self
)
```

    
Register /preview endpoint.

    
#### register_routes

```python3
def register_routes(
    self
)
```

    
This Method register routes to the router.

Because we wrap the endpoints in a class we cannot define the routes as
methods (because of the self argument). The HACK is to define routes inside
the class method and register them after the class initialization.

    
#### statistics

```python3
def statistics(
    self
)
```

    
add statistics endpoints.

    
#### tile

```python3
def tile(
    self
)
```

    
Register /tiles endpoint.

    
#### tilejson

```python3
def tilejson(
    self
)
```

    
Register /tilejson.json endpoint.

    
#### tms_dependency

```python3
def tms_dependency(
    TileMatrixSetId: titiler.core.dependencies.TileMatrixSetName = Query(TileMatrixSetName.WebMercatorQuad)
) -> morecantile.models.TileMatrixSet
```

    
TileMatrixSet Dependency.

    
#### url_for

```python3
def url_for(
    self,
    request: starlette.requests.Request,
    name: str,
    **path_params: Any
) -> str
```

    
Return full url (with prefix) for a specific endpoint.

    
#### wmts

```python3
def wmts(
    self
)
```

    
Register /wmts endpoint.

### MultiBaseTilerFactory

```python3
class MultiBaseTilerFactory(
    reader: Type[rio_tiler.io.base.MultiBaseReader] = <class 'rio_tiler.io.cogeo.COGReader'>,
    router: fastapi.routing.APIRouter = <factory>,
    path_dependency: Callable[..., Any] = <function DatasetPathParams at 0x7fe57c81aa60>,
    dataset_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.DatasetParams'>,
    layer_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.AssetsBidxExprParams'>,
    render_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.ImageRenderingParams'>,
    colormap_dependency: Callable[..., Union[Dict[int, Tuple[int, int, int, int]], Sequence[Tuple[Tuple[Union[float, int], Union[float, int]], Tuple[int, int, int, int]]], NoneType]] = <function ColorMapParams at 0x7fe57ca0d040>,
    stats_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.StatisticsParams'>,
    histogram_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.HistogramParams'>,
    process_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.PostProcessParams'>,
    tms_dependency: Callable[..., morecantile.models.TileMatrixSet] = <function TMSParams at 0x7fe57f43d700>,
    reader_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.DefaultDependency'>,
    router_prefix: str = '',
    gdal_config: Dict = <factory>,
    optional_headers: List[titiler.core.resources.enums.OptionalHeader] = <factory>,
    route_dependencies: List[Tuple[List[titiler.core.routing.EndpointScope], List[fastapi.params.Depends]]] = <factory>,
    img_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.ImageParams'>,
    add_preview: bool = True,
    add_part: bool = True,
    assets_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.AssetsParams'>
)
```

#### Ancestors (in MRO)

* titiler.core.factory.TilerFactory
* titiler.core.factory.BaseTilerFactory

#### Class variables

```python3
add_part
```

```python3
add_preview
```

```python3
assets_dependency
```

```python3
dataset_dependency
```

```python3
histogram_dependency
```

```python3
img_dependency
```

```python3
layer_dependency
```

```python3
process_dependency
```

```python3
reader
```

```python3
reader_dependency
```

```python3
render_dependency
```

```python3
router_prefix
```

```python3
stats_dependency
```

#### Methods

    
#### add_route_dependencies

```python3
def add_route_dependencies(
    self,
    *,
    scopes: List[titiler.core.routing.EndpointScope],
    dependencies=typing.List[fastapi.params.Depends]
)
```

    
Add dependencies to routes.

Allows a developer to add dependencies to a route after the route has been defined.

    
#### bounds

```python3
def bounds(
    self
)
```

    
Register /bounds endpoint.

    
#### colormap_dependency

```python3
def colormap_dependency(
    colormap_name: titiler.core.dependencies.ColorMapName = Query(None),
    colormap: str = Query(None)
) -> Union[Dict[int, Tuple[int, int, int, int]], Sequence[Tuple[Tuple[Union[float, int], Union[float, int]], Tuple[int, int, int, int]]], NoneType]
```

    
Colormap Dependency.

    
#### info

```python3
def info(
    self
)
```

    
Register /info endpoint.

    
#### part

```python3
def part(
    self
)
```

    
Register /crop endpoint.

    
#### path_dependency

```python3
def path_dependency(
    url: str = Query(Ellipsis)
) -> str
```

    
Create dataset path from args

    
#### point

```python3
def point(
    self
)
```

    
Register /point endpoints.

    
#### preview

```python3
def preview(
    self
)
```

    
Register /preview endpoint.

    
#### register_routes

```python3
def register_routes(
    self
)
```

    
This Method register routes to the router.

Because we wrap the endpoints in a class we cannot define the routes as
methods (because of the self argument). The HACK is to define routes inside
the class method and register them after the class initialization.

    
#### statistics

```python3
def statistics(
    self
)
```

    
Register /statistics endpoint.

    
#### tile

```python3
def tile(
    self
)
```

    
Register /tiles endpoint.

    
#### tilejson

```python3
def tilejson(
    self
)
```

    
Register /tilejson.json endpoint.

    
#### tms_dependency

```python3
def tms_dependency(
    TileMatrixSetId: titiler.core.dependencies.TileMatrixSetName = Query(TileMatrixSetName.WebMercatorQuad)
) -> morecantile.models.TileMatrixSet
```

    
TileMatrixSet Dependency.

    
#### url_for

```python3
def url_for(
    self,
    request: starlette.requests.Request,
    name: str,
    **path_params: Any
) -> str
```

    
Return full url (with prefix) for a specific endpoint.

    
#### wmts

```python3
def wmts(
    self
)
```

    
Register /wmts endpoint.

### TMSFactory

```python3
class TMSFactory(
    supported_tms: Type[titiler.core.dependencies.TileMatrixSetName] = <enum 'TileMatrixSetName'>,
    tms_dependency: Callable[..., morecantile.models.TileMatrixSet] = <function TMSParams at 0x7fe57f43d700>,
    router: fastapi.routing.APIRouter = <factory>,
    router_prefix: str = ''
)
```

#### Class variables

```python3
router_prefix
```

```python3
supported_tms
```

#### Methods

    
#### register_routes

```python3
def register_routes(
    self
)
```

    
Register TMS endpoint routes.

    
#### tms_dependency

```python3
def tms_dependency(
    TileMatrixSetId: titiler.core.dependencies.TileMatrixSetName = Query(TileMatrixSetName.WebMercatorQuad)
) -> morecantile.models.TileMatrixSet
```

    
TileMatrixSet Dependency.

    
#### url_for

```python3
def url_for(
    self,
    request: starlette.requests.Request,
    name: str,
    **path_params: Any
) -> str
```

    
Return full url (with prefix) for a specific endpoint.

### TilerFactory

```python3
class TilerFactory(
    reader: Type[rio_tiler.io.base.BaseReader] = <class 'rio_tiler.io.cogeo.COGReader'>,
    router: fastapi.routing.APIRouter = <factory>,
    path_dependency: Callable[..., Any] = <function DatasetPathParams at 0x7fe57c81aa60>,
    dataset_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.DatasetParams'>,
    layer_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.BidxExprParams'>,
    render_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.ImageRenderingParams'>,
    colormap_dependency: Callable[..., Union[Dict[int, Tuple[int, int, int, int]], Sequence[Tuple[Tuple[Union[float, int], Union[float, int]], Tuple[int, int, int, int]]], NoneType]] = <function ColorMapParams at 0x7fe57ca0d040>,
    stats_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.StatisticsParams'>,
    histogram_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.HistogramParams'>,
    process_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.PostProcessParams'>,
    tms_dependency: Callable[..., morecantile.models.TileMatrixSet] = <function TMSParams at 0x7fe57f43d700>,
    reader_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.DefaultDependency'>,
    router_prefix: str = '',
    gdal_config: Dict = <factory>,
    optional_headers: List[titiler.core.resources.enums.OptionalHeader] = <factory>,
    route_dependencies: List[Tuple[List[titiler.core.routing.EndpointScope], List[fastapi.params.Depends]]] = <factory>,
    img_dependency: Type[titiler.core.dependencies.DefaultDependency] = <class 'titiler.core.dependencies.ImageParams'>,
    add_preview: bool = True,
    add_part: bool = True
)
```

#### Ancestors (in MRO)

* titiler.core.factory.BaseTilerFactory

#### Descendants

* titiler.core.factory.MultiBaseTilerFactory
* titiler.core.factory.MultiBandTilerFactory

#### Class variables

```python3
add_part
```

```python3
add_preview
```

```python3
dataset_dependency
```

```python3
histogram_dependency
```

```python3
img_dependency
```

```python3
layer_dependency
```

```python3
process_dependency
```

```python3
reader
```

```python3
reader_dependency
```

```python3
render_dependency
```

```python3
router_prefix
```

```python3
stats_dependency
```

#### Methods

    
#### add_route_dependencies

```python3
def add_route_dependencies(
    self,
    *,
    scopes: List[titiler.core.routing.EndpointScope],
    dependencies=typing.List[fastapi.params.Depends]
)
```

    
Add dependencies to routes.

Allows a developer to add dependencies to a route after the route has been defined.

    
#### bounds

```python3
def bounds(
    self
)
```

    
Register /bounds endpoint.

    
#### colormap_dependency

```python3
def colormap_dependency(
    colormap_name: titiler.core.dependencies.ColorMapName = Query(None),
    colormap: str = Query(None)
) -> Union[Dict[int, Tuple[int, int, int, int]], Sequence[Tuple[Tuple[Union[float, int], Union[float, int]], Tuple[int, int, int, int]]], NoneType]
```

    
Colormap Dependency.

    
#### info

```python3
def info(
    self
)
```

    
Register /info endpoint.

    
#### part

```python3
def part(
    self
)
```

    
Register /crop endpoint.

    
#### path_dependency

```python3
def path_dependency(
    url: str = Query(Ellipsis)
) -> str
```

    
Create dataset path from args

    
#### point

```python3
def point(
    self
)
```

    
Register /point endpoints.

    
#### preview

```python3
def preview(
    self
)
```

    
Register /preview endpoint.

    
#### register_routes

```python3
def register_routes(
    self
)
```

    
This Method register routes to the router.

Because we wrap the endpoints in a class we cannot define the routes as
methods (because of the self argument). The HACK is to define routes inside
the class method and register them after the class initialization.

    
#### statistics

```python3
def statistics(
    self
)
```

    
add statistics endpoints.

    
#### tile

```python3
def tile(
    self
)
```

    
Register /tiles endpoint.

    
#### tilejson

```python3
def tilejson(
    self
)
```

    
Register /tilejson.json endpoint.

    
#### tms_dependency

```python3
def tms_dependency(
    TileMatrixSetId: titiler.core.dependencies.TileMatrixSetName = Query(TileMatrixSetName.WebMercatorQuad)
) -> morecantile.models.TileMatrixSet
```

    
TileMatrixSet Dependency.

    
#### url_for

```python3
def url_for(
    self,
    request: starlette.requests.Request,
    name: str,
    **path_params: Any
) -> str
```

    
Return full url (with prefix) for a specific endpoint.

    
#### wmts

```python3
def wmts(
    self
)
```

    
Register /wmts endpoint.