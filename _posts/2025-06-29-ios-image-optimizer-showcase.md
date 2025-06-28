---
layout: single
title: "Building iOS Image Optimizer: A Developer's Tool for App Bundle Optimization"
date: 2025-06-28
categories: [iOS Development, Swift, Developer Tools]
tags: [ios-optimization, command-line-tool, swift-package, app-bundle, image-optimization, developer-productivity]
header:
  teaser: /assets/images/iOS-image-optimizer-banner.jpg
  image: /assets/images/iOS-image-optimizer-banner.jpg
---

## iOS Image Optimizer: Streamlining App Bundle Management

iOS apps often accumulate unused images and oversized assets over time, leading to bloated app bundles. I created **iOS Image Optimizer**, a command-line tool that helps iOS developers identify and eliminate wasted space in their projects.

### The Problem

iOS projects accumulate unnecessary images from design iterations, removed features, and multiple resolution variants. This creates:

- Bundle bloat and slower downloads
- App Store review delays  
- Wasted storage on user devices
- Maintenance overhead

Existing solutions were either too simple or overly complex for everyday development needs.

### What It Does

**Image Discovery**
- Scans standalone images (PNG, JPG, JPEG, PDF, SVG)
- Analyzes Asset Catalogs (@1x, @2x, @3x variants)
- Recursive directory traversal

**Usage Detection**
- Swift: `UIImage(named:)`, `Image("name")`, SF Symbols
- Objective-C: `[UIImage imageNamed:]` patterns
- Interface Builder: Storyboards and XIB files

**Size Analysis**
- 1x images: Under 100 KB recommended
- 2x images: Under 200 KB recommended  
- 3x images: Under 400 KB recommended

**Reporting**
- Color-coded terminal output
- Detailed file paths and potential savings
- JSON export for automation

### Technical Implementation

**Swift Package Architecture**

```swift
let package = Package(
    name: "iOSImageOptimizer",
    platforms: [.macOS(.v13)],
    dependencies: [
        .package(url: "https://github.com/apple/swift-argument-parser", from: "1.3.0"),
        .package(url: "https://github.com/JohnSundell/Files", from: "4.0.0"),
        .package(url: "https://github.com/onevcat/Rainbow", from: "4.0.0")
    ]
)
```

**Command-Line Interface**

```swift
struct IOSImageOptimizer: ParsableCommand {
    @Argument(help: "Path to iOS project directory")
    var projectPath: String
    
    @Flag(name: .shortAndLong, help: "Show detailed output")
    var verbose = false
    
    @Flag(name: .shortAndLong, help: "Export findings to JSON")
    var json = false
    
    mutating func run() throws {
        let analyzer = ProjectAnalyzer(projectPath: projectPath, verbose: verbose)
        let report = try analyzer.analyze()
        
        json ? try report.exportJSON() : report.printToConsole()
    }
}
```

**Image Scanner**

```swift
class ImageScanner {
    func scanForImages() throws -> [ImageAsset] {
        var images: [ImageAsset] = []
        let folder = try Folder(path: projectPath)
        
        images.append(contentsOf: try scanStandaloneImages(in: folder))
        images.append(contentsOf: try scanAssetCatalogs(in: folder))
        
        return images
    }
}
```

**Usage Detection with Regex**

```swift
private func findImageReferences(in content: String, fileType: FileType) -> Set<String> {
    let patterns: [String]
    
    switch fileType {
    case .swift:
        patterns = [
            #"UIImage\s*\(\s*named:\s*"([^"]+)""#,
            #"Image\s*\(\s*"([^"]+)""#,
            #"UIImage\s*\(\s*systemName:\s*"([^"]+)""#
        ]
    case .objectiveC:
        patterns = [#"\[UIImage\s+imageNamed:\s*@"([^"]+)""#]
    case .interfaceBuilder:
        patterns = [#"image="([^"]+)""#, #"imageName="([^"]+)""#]
    }
    
    // Apply regex patterns and extract matches
    return extractImageNames(from: content, using: patterns)
}
```

### Key Challenges Solved

1. **Complex iOS project structures** - Used Files library for robust recursive traversal
2. **Asset Catalog parsing** - Handle nested .xcassets with JSON metadata
3. **Dynamic image loading** - Comprehensive regex patterns with manual verification option
4. **Performance optimization** - Efficient file filtering and compiled regex patterns

### Real-World Results

Testing across various projects showed:
- **15-25% unused images** found on average
- **800KB to 3MB** typical size savings
- **10-second analysis** vs 30+ minutes manual checking

### Architecture Highlights

**Clean separation of concerns:**
- `ImageScanner`: File discovery and enumeration
- `UsageDetector`: Code analysis and pattern matching
- `ProjectAnalyzer`: Orchestration and business logic
- `AnalysisReport`: Formatting and output

### Phase 2 Features (Coming Soon)

- Automated image compression
- Duplicate detection
- Xcode plugin integration
- CI/CD automation

### Try It Yourself

**Clone and Build:**
```bash
git clone https://github.com/sahilsatralkar/iOSImageOptimizer.git
cd iOSImageOptimizer/iOSImageOptimizer
swift build
```

**Run Analysis:**
```bash
swift run iOSImageOptimizer /path/to/your/ios/project --verbose
```

**GitHub Repository:** [iOS Image Optimizer](https://github.com/sahilsatralkar/iOSImageOptimizer)

The project is open source and welcomes contributions. Whether you find bugs, have feature requests, or want to contribute code, your involvement helps make this tool better for the entire iOS development community.

---

*iOS Image Optimizer represents Phase 1 of my vision for comprehensive app optimization tools. With community feedback and contributions, it has the potential to become an essential part of every iOS developer's workflow.*