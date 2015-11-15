// Telegram message decoding
$telegramMsg = file_get_contents('php://input');
$messageobj = json_decode($telegramMsg, true);
$chat_id = $messageobj['message']['chat']['id'];
$message_txt_parts = explode(' ', $messageobj['message']['text']);
$sender = $messageobj['message']['from']['username'];

// Checking if a username has been set
if (empty($sender)) {
$this->_sendback_message($chat_id, "You do not have a username setup on your profile. Please setup a username on your profile to be able to use commands on this.");
return;
}

switch ($message_txt_parts[0]) {
case '/creatematch':
// Use the telegram message parts, validate and add to db
// Return here the result of what you want the group to see
// Sample
// $this->_sendback_message($chat_id, "Match created successfully.");
// return;
break;
case '/changelocation':
// Do which ever you wanna do here and return a message
break;
case '/games':
// Do which ever you wanna do here and return a message
break;
case '/deletematch':
// Do which ever you wanna do here and return a message
break;
case '/yes':
// Do which ever you wanna do here and return a message
break;
}

}

private function _sendback_message($chat_id, $text_message)
{
$messageArray['chat_id'] = $chat_id;
$messageArray['text'] = $text_message;
$returnMsgURL = 'https://api.telegram.org/HERE-WILL-BE-YOUR-BOT-API-KEY/sendMessage';
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $returnMsgURL);
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($messageArray));
curl_setopt($ch, CURLOPT_HTTPHEADER, array('Content-Type: application/x-www-form-urlencoded'));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
$result = curl_exec($ch);
curl_close($ch);
