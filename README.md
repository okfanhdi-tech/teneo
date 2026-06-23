Đoạn mã SDK — TypeScript (@teneo-protocol/sdk)


import { TeneoSDK, SecurePrivateKey } from "@teneo-protocol/sdk";

const sdk = new TeneoSDK({
  wsUrl: "wss://backend.developer.chatroom.teneo-protocol.ai/ws",
  privateKey: new SecurePrivateKey(process.env.PRIVATE_KEY!),
  autoSummon: true // Automatically add agents to rooms when needed
});

await sdk.connect();

// Get your rooms (private rooms are available immediately after auth)
const rooms = sdk.getRooms();
const myRoom = rooms.find(r => r.is_owner);

// This is a free command — no payment required
const response = await sdk.sendMessage("@__example__ /summarize 50", {
  room: myRoom!.id,
  waitForResponse: true,
  timeout: 30000
});

console.log(response.content);

sdk.disconnect();

// If you prefer not to enable autoSummon globally, you can add agents manually:
//
// await sdk.agentRoom.addAgentToRoom(myRoom!.id, "__example__");
// const response = await sdk.sendMessage("@__example__ /summarize 50", { ... });
