# University-companion-App-
The University companion app is a mobile application designed to help students, faculty, and staff manage and stay informed about university events such as workshops, seminars, cultural programs, sports events, academic deadlines, and more.


import 'package:flutter/material.dart';
import 'package:carousel_slider/carousel_slider.dart';


void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'University App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  final List<String> eventImages = [
    'https://www.au.edu.pk/images/banner2.jpg',
    'https://www.au.edu.pk/images/banner1.jpg',
    'https://www.au.edu.pk/images/banner3.jpg'
  ];

  final List<String> clubImages = [
    'https://www.au.edu.pk/images/club1.jpg',
    'https://www.au.edu.pk/images/club2.jpg',
    'https://www.au.edu.pk/images/club3.jpg'
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('AIR University'),
        leading: Builder(
          builder: (context) => IconButton(
            icon: Icon(Icons.menu),
            onPressed: () {
              Scaffold.of(context).openDrawer();
            },
          ),
        ),
      ),
      drawer: Drawer(
        child: ListView(
          children: [
            DrawerHeader(
              decoration: BoxDecoration(color: Colors.blue),
              child: Text(
                'Menu',
                style: TextStyle(color: Colors.white, fontSize: 24),
              ),
            ),
            ListTile(
              leading: Icon(Icons.event),
              title: Text('Register for Club'),
              onTap: () {
                // Navigate to registration page
              },
            ),
            ListTile(
              leading: Icon(Icons.event_available),
              title: Text('Check Events'),
              onTap: () {
                // Navigate to events page
              },
            ),
          ],
        ),
      ),
      body: SingleChildScrollView(
        child: Column(
          children: [
            // Slideshow for events
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                children: [
                  Text(
                    'Upcoming Events',
                    style: TextStyle(
                      fontSize: 20,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  SizedBox(height: 10),
                  CarouselSlider(
                    options: CarouselOptions(height: 200, autoPlay: true),
                    items: eventImages.map((url) {
                      return Builder(
                        builder: (BuildContext context) {
                          return Container(
                            width: MediaQuery.of(context).size.width,
                            margin: EdgeInsets.symmetric(horizontal: 5.0),
                            decoration: BoxDecoration(color: Colors.amber),
                            child: Image.network(url, fit: BoxFit.cover),
                          );
                        },
                      );
                    }).toList(),
                  ),
                  TextButton(
                    onPressed: () {
                      // Navigate to all events
                    },
                    child: Text('See More'),
                  ),
                ],
              ),
            ),

            // Slideshow for societies
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                children: [
                  Text(
                    'Societies',
                    style: TextStyle(
                      fontSize: 20,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  SizedBox(height: 10),
                  CarouselSlider(
                    options: CarouselOptions(height: 200, autoPlay: true),
                    items: clubImages.map((url) {
                      return Builder(
                        builder: (BuildContext context) {
                          return Container(
                            width: MediaQuery.of(context).size.width,
                            margin: EdgeInsets.symmetric(horizontal: 5.0),
                            decoration: BoxDecoration(color: Colors.blue),
                            child: Image.network(url, fit: BoxFit.cover),
                          );
                        },
                      );
                    }).toList(),
                  ),
                  TextButton(
                    onPressed: () {
                      // Navigate to all societies
                    },
                    child: Text('See More'),
                  ),
                ],
              ),
            ),

            // Bottom sections
            Padding(
              padding: const EdgeInsets.all(8.0),
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children: [
                  _buildSectionButton(context, Icons.event, 'Events', () {
                    // Navigate to events page
                  }),
                  _buildSectionButton(context, Icons.group, 'Clubs', () {
                    // Navigate to clubs page
                  }),
                  _buildSectionButton(context, Icons.person, 'My Profile', () {
                    // Navigate to profile page
                  }),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }

  Widget _buildSectionButton(BuildContext context, IconData icon, String label, VoidCallback onPressed) {
    return Column(
      children: [
        IconButton(
          icon: Icon(icon, size: 30),
          onPressed: onPressed,
        ),
        Text(label, style: TextStyle(fontSize: 14)),
      ],
    );
  }
}

