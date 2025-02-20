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
