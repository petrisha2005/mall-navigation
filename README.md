# mall-navigation
import 'package:flutter/material.dart';
import 'package:flutter_dotenv/flutter_dotenv.dart';
import 'package:maplibre_gl/mapbox_gl.dart';

Future<void> main() async {
  await dotenv.load(fileName: ".env");
  runApp(MallNavApp());
}

class MallNavApp extends StatelessWidget {
  const MallNavApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MallHomeWireframe(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class MallHomeWireframe extends StatelessWidget {
  const MallHomeWireframe({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text("Mall Navigation App"),
        backgroundColor: Colors.deepPurple,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            // 🔍 Search Bar
            Container(
              padding: const EdgeInsets.symmetric(horizontal: 12),
              decoration: BoxDecoration(
                color: Colors.white,
                border: Border.all(color: Colors.grey),
                borderRadius: BorderRadius.circular(10),
              ),
              child: Row(
                children: [
                  const Icon(Icons.search),
                  const SizedBox(width: 10),
                  const Expanded(
                    child: Text("Search for stores, places..."),
                  ),
                ],
              ),
            ),
            const SizedBox(height: 20),

            // 🗺️ MapLibre Map
            Expanded(
              child: MaplibreMap(
                styleString: "https://demotiles.maplibre.org/style.json", // free style
                initialCameraPosition: const CameraPosition(
                  target: LatLng(12.9716, 77.5946), // Example coords - Bangalore
                  zoom: 17.0,
                ),
                onMapCreated: (MaplibreMapController controller) {
                  // Optional: store controller for future use
                },
              ),
            ),
          ],
        ),
      ),
    );
  }
}
