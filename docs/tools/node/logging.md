# Node.js Logging

## Logging function in Node.js
```js
function writeLogInFile(message, object = false, fileName = 'node-server-custom-log.txt') {
  const getCircularReplacer = () => {
    const seen = new WeakSet();
    return (key, value) => {
      if (typeof value === "object" && value !== null) {
        if (seen.has(value)) return;
        seen.add(value);
      }
      return value;
    };
  };
  let filePath = `/var/log/zain-eshop/${fileName}`;
  let messageLog = "\r\n" + new Date().toLocaleString() + ' >> ';
  messageLog += object ? JSON.stringify(message, getCircularReplacer()) : message;
  if (fs.existsSync(filePath))
    fs.appendFile(filePath, messageLog, err => {
      if (err) throw err;
      console.log('The message was appended to : ' + filePath);
    });
  else
    fs.writeFile(filePath, messageLog, err => {
      if (err) throw err;
      console.log('The message was written to : ' + filePath);
    });
}
```
