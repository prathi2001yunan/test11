package com.component_demo.ui.theme.component
import android.os.Bundle
import androidx.activity.ComponentActivity
import androidx.activity.compose.setContent
import androidx.compose.foundation.Image
import androidx.compose.foundation.background
import androidx.compose.foundation.border
import androidx.compose.foundation.layout.Arrangement
import androidx.compose.foundation.layout.Box
import androidx.compose.foundation.layout.Column
import androidx.compose.foundation.layout.Row
import androidx.compose.foundation.layout.Spacer
import androidx.compose.foundation.layout.fillMaxSize
import androidx.compose.foundation.layout.fillMaxWidth
import androidx.compose.foundation.layout.height
import androidx.compose.foundation.layout.padding
import androidx.compose.foundation.layout.size
import androidx.compose.foundation.layout.width
import androidx.compose.foundation.lazy.LazyColumn
import androidx.compose.foundation.shape.RoundedCornerShape
import androidx.compose.foundation.text.KeyboardOptions
import androidx.compose.material.icons.Icons
import androidx.compose.material.icons.filled.KeyboardArrowDown
import androidx.compose.material3.Button
import androidx.compose.material3.ButtonDefaults
import androidx.compose.material3.Divider
import androidx.compose.material3.DropdownMenu
import androidx.compose.material3.DropdownMenuItem
import androidx.compose.material3.ExperimentalMaterial3Api
import androidx.compose.material3.ExposedDropdownMenuBox
import androidx.compose.material3.ExposedDropdownMenuDefaults
import androidx.compose.material3.Icon
import androidx.compose.material3.IconButton
import androidx.compose.material3.MaterialTheme
import androidx.compose.material3.Scaffold
import androidx.compose.material3.Text
import androidx.compose.material3.TextButton
import androidx.compose.material3.TextField
import androidx.compose.material3.TextFieldDefaults
import androidx.compose.material3.TopAppBar
import androidx.compose.material3.TopAppBarDefaults
import androidx.compose.runtime.Composable
import androidx.compose.runtime.getValue
import androidx.compose.runtime.mutableStateOf
import androidx.compose.runtime.remember
import androidx.compose.runtime.saveable.rememberSaveable
import androidx.compose.runtime.setValue
import androidx.compose.ui.Alignment
import androidx.compose.ui.ExperimentalComposeUiApi
import androidx.compose.ui.Modifier
import androidx.compose.ui.draw.clip
import androidx.compose.ui.draw.shadow
import androidx.compose.ui.graphics.Color
import androidx.compose.ui.platform.LocalContext
import androidx.compose.ui.platform.LocalDensity
import androidx.compose.ui.platform.LocalSoftwareKeyboardController
import androidx.compose.ui.res.painterResource
import androidx.compose.ui.text.font.FontWeight
import androidx.compose.ui.text.input.ImeAction
import androidx.compose.ui.tooling.preview.Preview
import androidx.compose.ui.unit.dp
import androidx.compose.ui.unit.sp
import com.example.simple.ui.theme.SimpleTheme

class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            QualificationForm()

        }
    }
}

@Composable
fun QualificationForm() {
    Scaffold(topBar = {
        QualificationFormTopBar()
    }, bottomBar = {
        QualificationFormBottomBar()
    }) { paddingValues ->
        // rest of the app's UI
        LazyColumn(
            modifier = Modifier
                .fillMaxSize()
                .padding(paddingValues = paddingValues)
                .padding(top = 20.dp),
            verticalArrangement = Arrangement.Top,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
            item {
                Text(
                    text = "Training & education",
                    style = MaterialTheme.typography.headlineLarge,
                    color = MaterialTheme.colorScheme.onPrimary
                )
                Spacer(modifier = Modifier.height(10.dp))
                Text(
                    text = "Please enter your qualification details",
                    style = MaterialTheme.typography.displaySmall,
                    color = Color(0xFFB6B2B2)
                )
                Spacer(modifier = Modifier.height(40.dp))
                ExposedDropdownMenu(false)
                Spacer(modifier = Modifier.height(15.dp))
                TextFieldComponent(
                    text = "Field of study",
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(horizontal = 20.dp)
                        .height(60.dp),
                    color = Color(0xFFF3F3F3)
                )
                Spacer(modifier = Modifier.height(23.dp))
                Divider(
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(horizontal = 20.dp),
                    color = MaterialTheme.colorScheme.secondary
                )
                Spacer(modifier = Modifier.height(23.dp))
                TextFieldComponent(
                    text = "Training Experience",
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(horizontal = 20.dp)
                        .height(60.dp),
                    color = Color(0xFFF3F3F3)
                )
            }
            }
        }
    }


@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun QualificationFormTopBar() {
    TopAppBar(title = {
        Row(
            Modifier
                .fillMaxWidth()
                .padding(start = 50.dp),
            Arrangement.Center,
            Alignment.CenterVertically
        ) {
            Image(
                painter = painterResource(id = R.drawable.ic_launcher_background),
                contentDescription = "",
                modifier = Modifier.size(70.dp)
            )
        }
    }, actions = {
        TextButton(onClick = { /* do something */ }) {
            Text("CANCEL", style = MaterialTheme.typography.displayMedium , color = MaterialTheme.colorScheme.primary)
        }
    }, colors = TopAppBarDefaults.largeTopAppBarColors(MaterialTheme.colorScheme.background))
}


@Composable
fun QualificationFormBottomBar() {
    Row(
        modifier = Modifier
            .fillMaxWidth()
            .padding(horizontal = 20.dp)
            .padding(bottom = 20.dp)
    ) {
        Button(
            onClick = { /*TODO*/ },
            modifier = Modifier
                .fillMaxWidth()
                .height(70.dp)
                .shadow(
                    elevation = 5.dp,
                    ambientColor = Color(0xFFEF0634),
                    spotColor = Color(0xFFEF0634),
                    shape = RoundedCornerShape(20.dp)
                ),
            colors = ButtonDefaults.buttonColors(Color(0xFFEF0634))
        ) {
            Text(text = "SAVE", fontSize = 17.sp, color = Color.White, fontWeight = FontWeight.Bold)
        }
    }
}


@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun TextFieldComponent(
    text: String, modifier: Modifier, color: Color, withBorder: Boolean = false
) {
    TextField(value = "",
        onValueChange = {},
        modifier = modifier
            .clip(RoundedCornerShape(5.dp))
            .border(
                2.dp,
                if (withBorder) Color(0xFFD1CCCC) else Color.Transparent,
                RoundedCornerShape(5.dp)
            ),
        colors = TextFieldDefaults.textFieldColors(
            containerColor = color,
            focusedIndicatorColor = Color(0xFFF1F0FF),
            unfocusedIndicatorColor = Color(0xFFF1F0FF)
        ),
        placeholder = {
            Text(
                text = text, style = MaterialTheme.typography.displaySmall, fontWeight = FontWeight.W600,
                color = MaterialTheme.colorScheme.onPrimaryContainer
            )
        },
        singleLine = true,
    )
}

@Composable
fun BoxComponent() {
    Box(modifier = Modifier
        .height(30.dp)
        .width(20.dp)
        .clip(RoundedCornerShape(10.dp))
        .background(
            Color.Red,
            RoundedCornerShape(10.dp)
        )) {

    }
}




@OptIn(ExperimentalMaterial3Api::class)
@Composable
fun ExposedDropdownMenu(withBorder: Boolean = false) {

    var expanded by remember {
        mutableStateOf(false)
    }

    var selectedItem by remember {
        mutableStateOf("")
    }

    ExposedDropdownMenuBox(
        expanded = expanded,
        onExpandedChange = { newValue ->
           expanded = newValue
        },
        modifier = Modifier.fillMaxWidth()
            .padding(horizontal = 20.dp)
    ) {
        TextField(
            value = selectedItem,
            onValueChange = { },
            modifier = Modifier.fillMaxWidth()
                .height(60.dp)
                .clip(RoundedCornerShape(5.dp))
                .border(
                    2.dp,
                    Color.Transparent,
                    RoundedCornerShape(5.dp)
                )
                .menuAnchor(),
            colors = TextFieldDefaults.textFieldColors(
                containerColor = Color(
                    0xFFF3F3F3
                ),
                focusedIndicatorColor = Color(0xFFF1F0FF),
                unfocusedIndicatorColor = Color(0xFFF1F0FF)
            ),
            placeholder = {
                Text(
                    text = "Degree / diploma / certificate",
                    fontSize = 25.sp,
                    fontWeight = FontWeight.W600,
                    color = MaterialTheme.colorScheme.onPrimaryContainer
                )
            },
            trailingIcon = {
                ExposedDropdownMenuDefaults.TrailingIcon(expanded = expanded)

            },
            readOnly = true,
            keyboardOptions = KeyboardOptions.Default.copy(imeAction = ImeAction.None)
            )
        ExposedDropdownMenu(
            expanded = expanded,
            onDismissRequest = {
                expanded = false
            },
            modifier = Modifier.fillMaxWidth()) {
            DropdownMenuItem(
                text = {
                    Text(text = "Degree")
                },
                onClick = {
                    selectedItem = "Degree"
                    expanded = false
                }
            )
            DropdownMenuItem(
                text = {
                    Text(text = "diploma")
                },
                onClick = {
                    selectedItem = "diploma"
                    expanded = false
                }
            )
            DropdownMenuItem(
                text = {
                    Text(text = "certificate")
                },
                onClick = {
                    selectedItem = "certificate"
                    expanded = false
                }
            )
        }
    }
}

