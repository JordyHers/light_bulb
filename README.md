# Ligth Bulb 💡

The Light bulb project is actually famous among the community. It was originally made in
REACT Native and SwiftUI.

## Widgets involved.

- [Custom paint](https://api.flutter.dev/flutter/widgets/CustomPaint-class.html)

- [Draggable](https://api.flutter.dev/flutter/widgets/Draggable-class.html)

- [Canvas](https://api.flutter.dev/flutter/dart-ui/Canvas-class.html)

- [Position of the widget Offset](https://api.flutter.dev/flutter/dart-ui/Offset-class.html)

## Live Demo

<img width="515" alt="lightScreen" src="https://user-images.githubusercontent.com/49708438/179728639-db24b6da-b25a-4293-b9f9-043f0caa98c2.gif">

### The Bulb Container

```dart
Widget bulbContainer({Key? key}) {
    return InkWell(
      overlayColor: MaterialStateProperty.all(Colors.transparent),
      onTap: () {
        setState(() {
          isLightOn = !isLightOn;
        });
      },
      child: Container(
        height: 100.0,
        color: Colors.transparent,
        child: Image.asset(
          isLightOn ? 'assets/on.png' : 'assets/off.png',
          fit: BoxFit.cover,
        ),
      ),
    );
  }
```

### The Wire

```dart
class Wire extends StatefulWidget {
  final Offset toOffset;
  final Offset initialPosition;

  const Wire({Key? key, required this.toOffset, required this.initialPosition})
      : super(key: key);
  @override
  State<StatefulWidget> createState() => _WireState();
}

class _WireState extends State<Wire> with SingleTickerProviderStateMixin {
  @override
  Widget build(BuildContext context) {
    return CustomPaint(
        painter: LinePainter(
          toOffset: widget.toOffset,
          initialPosition: widget.initialPosition,
        ));
  }
}

class LinePainter extends CustomPainter {
  Paint? _paint;
  final Offset initialPosition;
  final Offset toOffset;
  LinePainter({required this.toOffset, required this.initialPosition}) {
    _paint = Paint()
      ..color = lightColor
      ..strokeWidth = 2.0;
  }

  @override
  void paint(Canvas canvas, Size size) {
    canvas.drawLine(initialPosition, toOffset, _paint!);
  }

  @override
  bool shouldRepaint(LinePainter oldDelegate) {
    return false;
  }
}

```

## Tips

1- Add this line of code to hide unnecessary files

```dart
"explorer.fileNesting.enabled": true,
"explorer.fileNesting.expand": false,
"explorer.fileNesting.patterns": {
    "pubspec.yaml": ".flutter-plugins, .packages, .dart_tool, .flutter-plugins-dependencies, .metadata, .packages, pubspec.lock, build.yaml, analysis_options.yaml, all_lint_rules.yaml",
    ".gitignore": ".gitattributes, .gitmodules, .gitmessage, .mailmap, .git-blame*",
    "readme.*": "authors, backers.md, changelog*, citation*, code_of_conduct.md, codeowners, contributing.md, contributors, copying, credits, governance.md, history.md, license*, maintainers, readme*, security.md, sponsors.md",
    "*.dart": "$(capture).g.dart, $(capture).freezed.dart",
},
```

2- Add const automatically

```dart
"editor.codeActionsOnSave": {
    "source.fixAll": true
},
```

3- Remove red Error Pages

```dart
void main() {
ErrorWidget.builder =(FlutterErrorDetails details){
return const CustomErrorPage[];
    };
runApp(const MyApp());
 }
```

4- To see the live performance of apps and widgets

```dart
//Don't forget to run it in profile mode
MaterialApp(
    showperformanceOverlay: true
    )
 }
```

5- LayoutBuilder

```dart
LayoutBuilder(
    builder:(context,box){
        return Center(
            child: Text('${box.maxHeight.round()} ${box.maxWidth.round()}'),
        ),
    }
    )
 }
```

6- SwithListTile adaptive

```dart
//To run native icons and switches
    SwitchListTile.adaptive(
        title: const Text('Title')
        value:_isSelected,
        onChanged: onChanged,
        secondary:const Icon(Icons.adaptive.share)
    )
```
