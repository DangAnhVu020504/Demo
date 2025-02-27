package com.example.th2

import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.activity.enableEdgeToEdge
import androidx.compose.foundation.Image
import androidx.compose.foundation.layout.*
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material3.*
import androidx.compose.runtime.*
import androidx.compose.ui.Alignment
import androidx.compose.ui.Modifier
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.input.PasswordVisualTransformation
import androidx.compose.ui.text.input.KeyboardType
import androidx.compose.ui.text.style.TextAlign
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import com.example.th2.ui.theme.TH2Theme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        enableEdgeToEdge()
        setContent {
            TH2Theme {
                Scaffold(modifier = Modifier.fillMaxSize()) { innerPadding ->
                    Column(modifier = Modifier.padding(innerPadding)) {
                        /*SpringScreen()*/
                        Spacer(modifier = Modifier.height(20.dp))
                        LoginScreen()
                    }
                }
            }
        }
    }
}

@Composable
fun BMICalculator() {
    var name by remember { mutableStateOf("") }
    var weight by remember { mutableStateOf("") }
    var height by remember { mutableStateOf("") }
    var bmiResult by remember { mutableStateOf("") }
    var bmiCategory by remember { mutableStateOf("") }

    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp)
            .height(50.dp)
            .background(Color.White),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(
            text = "Chương trình tính chỉ số BMI",
            style = TextStyle(fontSize = 22.sp, fontWeight = FontWeight.Bold,)
        )

        Spacer(modifier = Modifier.height(20.dp))

        OutlinedTextField(
            value = name,
            onValueChange = { name = it },
            label = { Text("Nhập tên") },
            modifier = Modifier.fillMaxWidth()
        )

        Spacer(modifier = Modifier.height(10.dp))

        OutlinedTextField(
            value = height,
            onValueChange = { height = it },
            label = { Text("Chiều cao (m)") },
            keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Number),
            modifier = Modifier.fillMaxWidth()
        )

        Spacer(modifier = Modifier.height(10.dp))

        OutlinedTextField(
            value = weight,
            onValueChange = { weight = it },
            label = { Text("Cân nặng (kg)") },
            keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Number),
            modifier = Modifier.fillMaxWidth()
        )

        Spacer(modifier = Modifier.height(20.dp))

        Button(
            onClick = {
                val h = height.toFloatOrNull()
                val w = weight.toFloatOrNull()
                if (h != null && w != null && h > 0) {
                    val bmi = w / (h * h)
                    bmiResult = "Chỉ số BMI: %.2f".format(bmi)

                    bmiCategory = when {
                        bmi < 18 -> "Người gầy"
                        bmi < 25 -> "Người bình thường"
                        bmi < 30 -> "Béo phì độ I"
                        bmi < 35 -> "Béo phì độ II"
                        else -> "Béo phì độ III"
                    }
                } else {
                    bmiResult = "Vui lòng nhập đúng giá trị!"
                    bmiCategory = ""
                }
            },
            modifier = Modifier
                .fillMaxWidth(),
            colors = ButtonDefaults.buttonColors(
                containerColor = Color.Blue,
                contentColor = Color.Yellow
            )

        ) {
            Text(text = "Tính BMI", fontSize = 18.sp)
        }

        Spacer(modifier = Modifier.height(20.dp))

        Text(text = bmiResult, fontSize = 20.sp, fontWeight = FontWeight.Bold, color = Color.Blue)
        Text(text = bmiCategory, fontSize = 18.sp, fontWeight = FontWeight.Bold, color = Color.Red)
    }
}








/*@Composable
fun SpringScreen() {
    Column(
        modifier = Modifier.fillMaxWidth(),
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Image(
            painter = painterResource(id = R.drawable.), // Thay ảnh của bạn
            contentDescription = "Spring Image",
            modifier = Modifier.fillMaxWidth()
        )
        Text(
            text = "SPRING is coming",
            fontSize = 24.sp,
            color = Color.Black,
            textAlign = TextAlign.Center,
            modifier = Modifier.padding(top = 16.dp)
        )
    }
}*/

@Composable
fun LoginScreen() {
    Column(
        modifier = Modifier
            .fillMaxSize()
            .padding(16.dp),
        horizontalAlignment = Alignment.CenterHorizontally,
        verticalArrangement = Arrangement.Center
    ) {
        Text(
            text = "ĐĂNG NHẬP HỆ THỐNG",
            fontSize = 26.sp,
            color = Color.Red,
            textAlign = TextAlign.Center,
            modifier = Modifier.padding(bottom = 20.dp)
        )

        var username by remember { mutableStateOf("") }
        var password by remember { mutableStateOf("") }

        TextField(
            value = username,
            onValueChange = { username = it },
            label = { Text("Tên đăng nhập") },
            modifier = Modifier.fillMaxWidth()
        )

        Spacer(modifier = Modifier.height(16.dp))

        TextField(
            value = password,
            onValueChange = { password = it },
            label = { Text("Mật khẩu") },
            visualTransformation = PasswordVisualTransformation(),
            keyboardOptions = KeyboardOptions(keyboardType = KeyboardType.Password),
            modifier = Modifier.fillMaxWidth()
        )

        Spacer(modifier = Modifier.height(16.dp))

        Button(
            onClick = { /* Xử lý đăng nhập */ },
            modifier = Modifier.fillMaxWidth()
        ) {
            Text(text = "ĐĂNG NHẬP")
        }
    }
}

@Preview(showBackground = true)
@Composable
fun PreviewScreens() {
    TH2Theme {
        Column {
           /* SpringScreen()*/
            LoginScreen()
        }
    }
}
