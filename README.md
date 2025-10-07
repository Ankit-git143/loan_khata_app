# loan_khata_app
Flutter app for managing loans &amp; borrow records
import 'package:flutter/material.dart';

void main() {
  runApp(LoanKhataApp());
}

class LoanKhataApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Loan Khata',
      theme: ThemeData(primarySwatch: Colors.green),
      home: LoanCalculatorPage(),
    );
  }
}

class LoanCalculatorPage extends StatefulWidget {
  @override
  _LoanCalculatorPageState createState() => _LoanCalculatorPageState();
}

class _LoanCalculatorPageState extends State<LoanCalculatorPage> {
  final principalController = TextEditingController();
  final interestController = TextEditingController();
  final timeController = TextEditingController();
  double result = 0;

  void calculateInterest() {
    final p = double.tryParse(principalController.text) ?? 0;
    final r = double.tryParse(interestController.text) ?? 0;
    final t = double.tryParse(timeController.text) ?? 0;
    setState(() {
      result = (p * r * t) / 100;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Loan Calculator')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(controller: principalController, decoration: InputDecoration(labelText: 'Principal Amount')),
            TextField(controller: interestController, decoration: InputDecoration(labelText: 'Interest Rate (%)')),
            TextField(controller: timeController, decoration: InputDecoration(labelText: 'Time (years)')),
            SizedBox(height: 16),
            ElevatedButton(onPressed: calculateInterest, child: Text('Calculate')),
            SizedBox(height: 16),
            Text('Simple Interest: ₹${result.toStringAsFixed(2)}', style: TextStyle(fontSize: 18)),
          ],
        ),
      ),
    );
  }
}
