import 'package:flutter/material.dart';

void main() => runApp(FutbolApp());

class FutbolApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Fútbol Argentino',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: PantallaInicio(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class PantallaInicio extends StatelessWidget {
  final Map<String, List<Map<String, String>>> partidos = {
    'Lunes': [
      {'local': 'River Plate', 'visitante': 'Boca Juniors', 'hora': '21:30'}
    ],
    'Martes': [
      {'local': 'Racing', 'visitante': 'Independiente', 'hora': '19:00'},
      {'local': 'San Lorenzo', 'visitante': 'Huracán', 'hora': '21:15'}
    ],
    'Miércoles': [
      {'local': 'Estudiantes', 'visitante': 'Gimnasia', 'hora': '20:00'}
    ],
    'Jueves': [
      {'local': 'Vélez', 'visitante': 'Lanús', 'hora': '19:30'},
      {'local': 'Talleres', 'visitante': 'Belgrano', 'hora': '21:45'}
    ],
    'Viernes': [
      {'local': 'Newells', 'visitante': 'Rosario Central', 'hora': '20:30'}
    ],
    'Sábado': [
      {'local': 'Godoy Cruz', 'visitante': 'Banfield', 'hora': '15:30'},
      {'local': 'Tigre', 'visitante': 'Platense', 'hora': '17:45'},
      {'local': 'Colón', 'visitante': 'Unión', 'hora': '20:00'}
    ],
    'Domingo': [
      {'local': 'Argentinos Juniors', 'visitante': 'Defensa y Justicia', 'hora': '15:00'},
      {'local': 'Arsenal', 'visitante': 'Sarmiento', 'hora': '17:30'},
      {'local': 'Atlético Tucumán', 'visitante': 'Central Córdoba', 'hora': '20:15'}
    ],
  };

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Partidos del Fútbol Argentino'),
        backgroundColor: Colors.blue[700],
        foregroundColor: Colors.white,
        centerTitle: true,
      ),
      body: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Colors.blue[50]!, Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: Padding(
          padding: EdgeInsets.all(16),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              SizedBox(height: 20),
              Text(
                'Selecciona un día de la semana',
                style: TextStyle(
                  fontSize: 22,
                  fontWeight: FontWeight.bold,
                  color: Colors.blue[800],
                ),
              ),
              SizedBox(height: 10),
              Text(
                'Toca cualquier día para ver los partidos',
                style: TextStyle(fontSize: 16, color: Colors.grey[600]),
              ),
              SizedBox(height: 20),
              Expanded(
                child: ListView.builder(
                  itemCount: partidos.keys.length,
                  itemBuilder: (context, index) {
                    String dia = partidos.keys.elementAt(index);
                    int cantidad = partidos[dia]!.length;
                    return Card(
                      margin: EdgeInsets.only(bottom: 12),
                      elevation: 3,
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(12),
                      ),
                      child: ListTile(
                        contentPadding: EdgeInsets.symmetric(horizontal: 20, vertical: 10),
                        leading: CircleAvatar(
                          backgroundColor: Colors.blue[100],
                          child: Icon(Icons.calendar_today, color: Colors.blue[700]),
                        ),
                        title: Text(
                          dia,
                          style: TextStyle(fontSize: 18, fontWeight: FontWeight.w600),
                        ),
                        subtitle: Text(
                          '$cantidad partido${cantidad > 1 ? 's' : ''}',
                          style: TextStyle(color: Colors.grey[600]),
                        ),
                        trailing: Icon(Icons.arrow_forward_ios, color: Colors.blue[700]),
                        onTap: () {
                          Navigator.push(
                            context,
                            MaterialPageRoute(
                              builder: (context) => PantallaPartidos(
                                dia: dia,
                                partidos: partidos[dia]!,
                              ),
                            ),
                          );
                        },
                      ),
                    );
                  },
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

class PantallaPartidos extends StatelessWidget {
  final String dia;
  final List<Map<String, String>> partidos;

  PantallaPartidos({required this.dia, required this.partidos});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(dia),
        backgroundColor: Colors.blue[700],
        foregroundColor: Colors.white,
      ),
      body: Container(
        decoration: BoxDecoration(
          gradient: LinearGradient(
            colors: [Colors.blue[50]!, Colors.white],
            begin: Alignment.topCenter,
            end: Alignment.bottomCenter,
          ),
        ),
        child: Padding(
          padding: EdgeInsets.all(16),
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.start,
            children: [
              SizedBox(height: 20),
              Text(
                'Partidos del $dia',
                style: TextStyle(
                  fontSize: 22,
                  fontWeight: FontWeight.bold,
                  color: Colors.blue[800],
                ),
              ),
              SizedBox(height: 10),
              Text(
                '${partidos.length} partido${partidos.length > 1 ? 's' : ''} programado${partidos.length > 1 ? 's' : ''}',
                style: TextStyle(fontSize: 16, color: Colors.grey[600]),
              ),
              SizedBox(height: 20),
              Expanded(
                child: ListView.builder(
                  itemCount: partidos.length,
                  itemBuilder: (context, index) {
                    final partido = partidos[index];
                    return Card(
                      margin: EdgeInsets.only(bottom: 16),
                      elevation: 4,
                      shape: RoundedRectangleBorder(
                        borderRadius: BorderRadius.circular(15),
                      ),
                      child: Container(
                        padding: EdgeInsets.all(20),
                        decoration: BoxDecoration(
                          borderRadius: BorderRadius.circular(15),
                          gradient: LinearGradient(
                            colors: [Colors.white, Colors.blue[25]!],
                            begin: Alignment.topLeft,
                            end: Alignment.bottomRight,
                          ),
                        ),
                        child: Row(
                          children: [
                            Expanded(
                              child: Column(
                                children: [
                                  Container(
                                    padding: EdgeInsets.all(12),
                                    decoration: BoxDecoration(
                                      color: Colors.blue[100],
                                      borderRadius: BorderRadius.circular(10),
                                    ),
                                    child: Icon(Icons.home, color: Colors.blue[700], size: 24),
                                  ),
                                  SizedBox(height: 8),
                                  Text(
                                    partido['local']!,
                                    style: TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
                                    textAlign: TextAlign.center,
                                  ),
                                  SizedBox(height: 4),
                                  Text('Local', style: TextStyle(fontSize: 12, color: Colors.grey[600])),
                                ],
                              ),
                            ),
                            Padding(
                              padding: EdgeInsets.symmetric(horizontal: 16),
                              child: Column(
                                children: [
                                  Text(
                                    'VS',
                                    style: TextStyle(
                                      fontSize: 18,
                                      fontWeight: FontWeight.bold,
                                      color: Colors.blue[700],
                                    ),
                                  ),
                                  SizedBox(height: 8),
                                  Container(
                                    padding: EdgeInsets.symmetric(horizontal: 12, vertical: 6),
                                    decoration: BoxDecoration(
                                      color: Colors.blue[700],
                                      borderRadius: BorderRadius.circular(20),
                                    ),
                                    child: Text(
                                      partido['hora']!,
                                      style: TextStyle(
                                        color: Colors.white,
                                        fontWeight: FontWeight.bold,
                                        fontSize: 14,
                                      ),
                                    ),
                                  ),
                                ],
                              ),
                            ),
                            Expanded(
                              child: Column(
                                children: [
                                  Container(
                                    padding: EdgeInsets.all(12),
                                    decoration: BoxDecoration(
                                      color: Colors.orange[100],
                                      borderRadius: BorderRadius.circular(10),
                                    ),
                                    child: Icon(Icons.flight_takeoff, color: Colors.orange[700], size: 24),
                                  ),
                                  SizedBox(height: 8),
                                  Text(
                                    partido['visitante']!,
                                    style: TextStyle(fontSize: 16, fontWeight: FontWeight.bold),
                                    textAlign: TextAlign.center,
                                  ),
                                  SizedBox(height: 4),
                                  Text('Visitante', style: TextStyle(fontSize: 12, color: Colors.grey[600])),
                                ],
                              ),
                            ),
                          ],
                        ),
                      ),
                    );
                  },
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
