# f290_acf_themes_and_navigation


```dart
import 'package:flutter/material.dart';

const Color darkBlue = Color.fromARGB(255, 18, 32, 47);

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  State<MyApp> createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  final light = ThemeData(primarySwatch: Colors.deepOrange);

  final dark = ThemeData.dark().copyWith(
      colorScheme: const ColorScheme.dark().copyWith(
        surface: Colors.white12,
        secondary: Colors.purple.shade200,
      ),
      switchTheme: SwitchThemeData(
        thumbColor: MaterialStateProperty.resolveWith<Color>((state) {
          if (state.contains(MaterialState.selected)) {
            return Colors.purple.shade200;
          } else {
            return Colors.white;
          }
        }),
        trackColor: MaterialStateProperty.resolveWith<Color>((state) {
          if (state.contains(MaterialState.selected)) {
            return Colors.purple.shade300;
          } else {
            return Colors.purple.shade100;
          }
        }),
      ));

  var isLightTheme = true;
  IconData icon = Icons.light_mode;

  var _swicth = true;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: isLightTheme ? light : dark,
      debugShowCheckedModeBanner: false,
      home: Scaffold(
        appBar: AppBar(
          title: Text('Themes'),
          actions: [
            IconButton(
                onPressed: () {
                  setState(() {
                    isLightTheme = !isLightTheme;
                    icon = isLightTheme ? Icons.light_mode : Icons.dark_mode;
                  });
                },
                icon: Icon(icon))
          ],
        ),
        body: Column(
          children: [
            AppCard(
              imageUrl:
                  'https://images.pexels.com/photos/210607/pexels-photo-210607.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
              description: 'Cotação de Ações',
            ),
            AppCard(
              imageUrl:
                  'https://images.pexels.com/photos/730547/pexels-photo-730547.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1',
              description: 'Cotação de Ações',
              callBack: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (BuildContext context) => Container(
                      color: Colors.red,
                    ),
                  ),
                );
              },
            ),
          ],
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(builder: (context) => const SecondRoute()),
            );
          },
          child: Icon(Icons.add),
        ),
      ),
    );
  }

  _buildComponents() {
    return Column(
      children: [
        Padding(
          padding: EdgeInsets.symmetric(horizontal: 16, vertical: 8),
          child: TextField(
            decoration: InputDecoration(
              filled: true,
              labelText: 'E-mail',
              helperText: 'E-mail valido, por favor',
            ),
          ),
        ),
        Text('Hello'),
        ElevatedButton(
          onPressed: () {},
          child: const Text('ElevatedButton'),
        ),
        TextButton(
          onPressed: () {},
          child: const Text('TextButton'),
        ),
        OutlinedButton(
          onPressed: () {},
          child: const Text('OutlinedButton'),
        ),
        IconButton(onPressed: () {}, icon: Icon(icon)),
        SwitchListTile(
          value: _swicth,
          onChanged: (bool value) {
            setState(() {
              _swicth = value;
            });
          },
        )
      ],
    );
  }
}

class AppCard extends StatelessWidget {
  final String imageUrl;
  final String description;
  final VoidCallback? callBack;

  const AppCard(
      {required this.imageUrl,
      required this.description,
      this.callBack});

  @override
  Widget build(BuildContext context) {
    return InkWell(
      onTap: callBack,
      child: Ink(
        child: Card(
          shape:
              RoundedRectangleBorder(borderRadius: BorderRadius.circular(10)),
          clipBehavior: Clip.antiAlias,
          child: Row(
            mainAxisAlignment: MainAxisAlignment.start,
            crossAxisAlignment: CrossAxisAlignment.center,
            children: [
              Image.network(
                imageUrl,
                height: 150,
                width: 150,
                fit: BoxFit.cover,
              ),
              Expanded(child: Text(description)),
            ],
          ),
        ),
      ),
    );
  }
}

class SecondRoute extends StatelessWidget {
  const SecondRoute({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Second Route'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: const Text('Go back!'),
        ),
      ),
    );
  }
}
```
