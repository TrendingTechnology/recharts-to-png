[![npm](https://img.shields.io/npm/v/recharts-to-png)](https://www.npmjs.com/package/recharts-to-png)
[![GitHub](https://img.shields.io/github/license/brammitch/recharts-to-png)](LICENSE)

# recharts-to-png

Uses [html2canvas](https://github.com/niklasvh/html2canvas) to convert a [Recharts](https://github.com/recharts/recharts) chart to PNG.

Inspired by these Stack Overflow questions and answers from [peter.bartos](https://stackoverflow.com/questions/45086005/recharts-component-to-png/56223127?noredirect=1#comment100914961_56223127) and [AlbertMunichMar](https://stackoverflow.com/questions/57206626/download-chart-as-png-format-in-react-without-overwriting-the-dom).

### Demo

See a [demo](https://csb-dyy8q.netlify.app/) using recharts-to-png alongside [FileSaver](https://www.npmjs.com/package/file-saver).

### Install

```
npm install recharts-to-png
```

### Usage

```javascript
// chart: Element | React.Component | AreaChart | BarChart | PieChart | etc.
await getPngData(chart);
```

Allows all [html2canvas configuration options](https://html2canvas.hertzen.com/configuration) to be passed:

```javascript
await getPngData(chart, options);
```

### Example

```javascript
function App() {
  // The chart that we want to download the PNG for.
  const [chart, setChart] = React.useState();

  const handleDownload = React.useCallback(async () => {
    if (chart !== undefined) {
      // Send the chart to getPngData
      const pngData = await getPngData(chart);
      // Use FileSaver to download the PNG
      FileSaver.saveAs(pngData, 'test.png');
    }
  }, [chart]);

  const data = [...];

  return (
    <>
      <LineChart
        ref={(ref) => setChart(ref)} // Set target element
        data={data}
        height={300}
        width={600}
      >
        <XAxis dataKey="name" />
        <YAxis />
        <CartesianGrid strokeDasharray="3 3" />
        <Tooltip />
        <Legend wrapperStyle={{ bottom: 0 }} />
        <Line type="monotone" dataKey="pv" stroke="#8884d8" activeDot={{ r: 8 }} />
        <Line type="monotone" dataKey="uv" stroke="#82ca9d" />
      </LineChart>
      <span style={{ float: 'left' }}>
        <button onClick={handleDownload}>Download</button>
      </span>
    </>
  );
}
```
