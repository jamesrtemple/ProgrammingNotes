# Common and Core Modules

## Lifecycle
AfterContentChecked, AfterContentInit, AfterViewChecked, AfterViewInit
DoCheck
OnChanges, OnInit, OnDestroy

## Angular Application Object
ApplicationRef, PlatformRef

## Change Detection
ChangeDetectionStrategy, ChangeDetectorRef, CollectionChangeRecord
DoCheck, OnChanges

DefaultIterableDiffer
KeyValueDiffer, KeyValueDifferFactory, KeyValueDiffers, KeyValueChangeRecord
IterableDiffer, IterableDifferFactory, IterableDiffers

SimpleChange, SimpleChanges (i)

## ES5 Class Shims
Class (f), ClassDefinition (i)

## Dependency Injection
ReflectiveInjector, @Host, @Inject, @Injectable, Injector, OpaqueToken,
@Optional, @Self, @SkipSelf, @TypeProvider, @ValueProvider

Provider (alias), TypeProvider, ValueProvider, ClassProvider,
ExistingProvider, FactoryProvider

## Compilation
Compiler

## Components and Directives
@Component, ComponentFactory, ComponentFactoryResolver, ComponentRef
@Directive, Input (i), Output (i), EventEmitter, ViewEncapsulation (E)


## Views and Querying and Accessing Content
@ContentChild, @ContentChildren, QueryList, ElementRef, Renderer,
Query, @ViewChildren, @ViewChild
Sanitizer, SecurityContext, TemplateRef, ViewContainerRef, ViewRef
(extends ChangeDetectorRef)

*COMMON* NgClass, NgStyle
*COMMON* NgFor, NgIf, NgSwitch, NgSwitchCase, NgSwitchDefault


## Error Handling
ErrorHandler

## Events
EventEmitter

## Services

## Pipes
Pipe (i), PipeTransform (i), WrappedValue

*COMMON* AsyncPipe, CurrencyPipe, DatePipe, DecimalPipe, JsonPipe,
*COMMON* LowerCasePipe, PercentPipe, SlicePipe, UpperCasePipe

## Modules
ModuleWithProviders (i), NgModule (i), NgModuleRef, NgModuleFactoryLoader

## Hell if I know
HostBinding, HostListener, TrackByFn, @Type (invoke as ES7 decorator)
VERSION, Version, enableProdMode (f)

*COMMON* APP_BASE_HREF
*COMMON* CommonModule (contains definitions for ngIf, ngFor...)

## Location / URL
*COMMON* HashLocationStrategy, Location, LocationStrategy, PlatformLocation,
*COMMON* PathLocationStrategy

