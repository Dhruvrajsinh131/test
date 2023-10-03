#replace all keys with snake_case


function replaceKeys(obj, keyMap) {
  if (typeof obj !== 'object') return obj;
  
  const result = Array.isArray(obj) ? [] : {};
  
  for (const key in obj) {
    const newKey = keyMap[key] || key;
    
    if (typeof obj[key] === 'object') {
      result[newKey] = replaceKeys(obj[key], keyMap);
    } else {
      result[newKey] = obj[key];
    }
  }
  
  return result;
}

const originalObject = {
  a: 1,
  b: {
    c: 2,
    d: 3
  },
  e: [4, 5, 6]
};

const keyMap = {
  a: 'x',
  c: 'y'
};

const modifiedObject = replaceKeys(originalObject, keyMap);

console.log(modifiedObject);
