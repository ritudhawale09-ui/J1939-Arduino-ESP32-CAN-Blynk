#include <SPI.h>
#include <mcp_can.h>

#define CS_PIN 10
#define POT_PIN A0
MCP_CAN CAN0(CS_PIN);

const uint32_t CAN_ID_ENGINE = 0x18FEF100;  // J1939 PGN for Engine Speed
const float MAX_RPM = 6000.0;

void setup() {
  Serial.begin(115200);
  Serial.println("=== ENGINE ECU (Arduino UNO) ===");
  // Init MCP2515
  while (CAN_OK != CAN0.begin(MCP_ANY, CAN_500KBPS, MCP_8MHZ)) {
    Serial.println("CAN init fail, retrying...");
    delay(1000);
  }
  CAN0.setMode(MCP_NORMAL);
  Serial.println("CAN init OK – sending engine speed...");
}

void loop() {
  int pot = analogRead(POT_PIN);
  float rpm = map(pot, 0, 1023, 0, MAX_RPM);
  uint16_t scaled = (uint16_t)(rpm / 0.125);   // J1939 scaling

  byte data[8] = { lowByte(scaled), highByte(scaled), 0, 0, 0, 0, 0, 0 };
  CAN0.sendMsgBuf(CAN_ID_ENGINE, 1, 8, data);

  Serial.print("Pot: "); Serial.print(pot);
  Serial.print(" | RPM: "); Serial.print(rpm);
  Serial.print(" | Data Sent: ");
  for (byte i=0;i<8;i++){ Serial.print(data[i],HEX); Serial.print(" "); }
  Serial.println();
  delay(200);
}


