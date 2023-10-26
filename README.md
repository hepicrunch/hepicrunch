import 'package:flutter/material.dart';

void main() => runApp(const MyApp());

class MyApp extends StatelessWidget {
  const MyApp({Key? key});

  @override
  Widget build(BuildContext context) {
    const appTitle = 'Absensi Mahasiswa';
    return MaterialApp(
      title: appTitle,
      home: Scaffold(
        appBar: AppBar(
          title: const Text(appTitle),
        ),
        body: MyCustomForm(),
      ),
    );
  }
}

class MyCustomForm extends StatefulWidget {
  MyCustomForm({Key? key}) : super(key: key);

  @override
  _MyCustomFormState createState() => _MyCustomFormState();
}

class _MyCustomFormState extends State<MyCustomForm> {
  String selectedDropdownValue = 'Kelas A';
  bool checkBoxValue = false;
  String radioGroupValue = 'Hadir';
  TextEditingController nameController = TextEditingController();
  TextEditingController usernameController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: <Widget>[
        Padding(
          padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 16),
          child: TextField(
            controller: nameController,
            decoration: InputDecoration(
              border: OutlineInputBorder(),
              hintText: 'Enter your name',
            ),
          ),
        ),
        Padding(
          padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 16),
          child: TextFormField(
            controller: usernameController,
            decoration: const InputDecoration(
              border: UnderlineInputBorder(),
              labelText: 'Enter your username',
            ),
          ),
        ),
        Padding(
          padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 16),
          child: DropdownButton<String>(
            value: selectedDropdownValue,
            onChanged: (String? newValue) {
              setState(() {
                selectedDropdownValue = newValue!;
              });
            },
            items: <String>['Kelas A', 'Kelas B', 'Kelas C', 'Kelas D']
                .map<DropdownMenuItem<String>>((String value) {
              return DropdownMenuItem<String>(
                value: value,
                child: Text(value),
              );
            }).toList(),
          ),
        ),
        Padding(
          padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 16),
          child: Row(
            children: <Widget>[
              Radio<String>(
                value: 'Hadir',
                groupValue: radioGroupValue,
                onChanged: (String? value) {
                  setState(() {
                    radioGroupValue = value!;
                  });
                },
              ),
              const Text('Hadir'),
              Radio<String>(
                value: 'Izin',
                groupValue: radioGroupValue,
                onChanged: (String? value) {
                  setState(() {
                    radioGroupValue = value!;
                  });
                },
              ),
              const Text('Izin'),
            ],
          ),
        ),
        Padding(
          padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 16),
          child: Row(
            children: <Widget>[
              Checkbox(
                value: checkBoxValue,
                onChanged: (bool? value) {
                  setState(() {
                    checkBoxValue = value!;
                  });
                },
              ),
              const Text('Saya Bertanggung jawab atas jawaban diatas'),
            ],
          ),
        ),
        Padding(
          padding: const EdgeInsets.symmetric(horizontal: 8, vertical: 16),
          child: ElevatedButton(
            onPressed: () {
              // Handle the submit action here
              String name = nameController.text;
              String username = usernameController.text;
              print('Name: $name, Username: $username');
              print('Selected Class: $selectedDropdownValue');
              print('Attendance Status: $radioGroupValue');
              print('Agreed to Terms: $checkBoxValue');
            },
            child: const Text('Submit'),
          ),
        ),
      ],
    );
  }
}
