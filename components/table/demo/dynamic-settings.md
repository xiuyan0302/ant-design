---
order: 21
title:
  en-US: Dynamic Settings
  zh-CN: 动态控制表格属性
---

## zh-CN

选择不同配置组合查看效果。

## en-US

Select different settings to see the result.

````jsx
import { Table, Icon, Switch, Radio, Form } from 'antd';
const FormItem = Form.Item;

const columns = [{
  title: 'Name',
  dataIndex: 'name',
  key: 'name',
  width: 150,
  render: text => <a href="#">{text}</a>,
}, {
  title: 'Age',
  dataIndex: 'age',
  key: 'age',
  width: 100,
}, {
  title: 'Address',
  dataIndex: 'address',
  key: 'address',
}, {
  title: 'Action',
  key: 'action',
  width: 400,
  render: (text, record) => (
    <span>
      <a href="#">Action 一 {record.name}</a>
      <span className="ant-divider" />
      <a href="#">Delete</a>
      <span className="ant-divider" />
      <a href="#" className="ant-dropdown-link">
        More actions<Icon type="down" />
      </a>
    </span>
  ),
}];

const data = [];
for (let i = 1; i <= 10; i++) {
  data.push({
    key: i,
    name: 'John Brown',
    age: `${i}2`,
    address: `New York No. ${i} Lake Park`,
    description: `My name is John Brown, I am ${i}2 years old, living in New York No. ${i} Lake Park.`,
  });
}

const expandedRowRender = record => <p>{record.description}</p>;
const title = () => 'Here is title';
const footer = () => 'Here is footer';
const scroll = { y: 240 };

class Demo extends React.Component {
  state = {
    bordered: true,
    loading: false,
    pagination: true,
    size: 'default',
    expandedRowRender,
    title,
    footer,
    rowSelection: {},
    scroll,
  }

  handleToggle = (prop) => {
    return (enable) => {
      this.setState({ [prop]: enable });
    };
  }

  handleSizeChange = (e) => {
    this.setState({ size: e.target.value });
  }

  handleExpandChange = (enable) => {
    this.setState({ expandedRowRender: enable ? expandedRowRender : false });
  }

  handleTitleChange = (enable) => {
    this.setState({ title: enable ? title : undefined });
  }

  handleFooterChange = (enable) => {
    this.setState({ footer: enable ? footer : undefined });
  }

  handleRowSelectionChange = (enable) => {
    this.setState({ rowSelection: enable ? {} : undefined });
  }

  handleScollChange = (enable) => {
    this.setState({ scroll: enable ? scroll : undefined });
  }

  render() {
    const state = this.state;
    return (
      <div>
        <div className="components-table-demo-control-bar">
          <Form inline>
            <FormItem label="Bordered">
              <Switch checked={state.bordered} onChange={this.handleToggle('bordered')} />
            </FormItem>
            <FormItem label="loading">
              <Switch checked={state.loading} onChange={this.handleToggle('loading')} />
            </FormItem>
            <FormItem label="Pagination">
              <Switch checked={state.pagination} onChange={this.handleToggle('pagination')} />
            </FormItem>
            <FormItem label="Title">
              <Switch defaultChecked onChange={this.handleTitleChange} />
            </FormItem>
            <FormItem label="Footer">
              <Switch defaultChecked onChange={this.handleFooterChange} />
            </FormItem>
            <FormItem label="Expandable">
              <Switch defaultChecked onChange={this.handleExpandChange} />
            </FormItem>
            <FormItem defaultChecked label="Checkbox">
              <Switch onChange={this.handleRowSelectionChange} />
            </FormItem>
            <FormItem label="Fixed Header">
              <Switch defaultChecked onChange={this.handleScollChange} />
            </FormItem>
            <FormItem label="Size">
              <Radio.Group value={state.size} onChange={this.handleSizeChange}>
                <Radio.Button value="default">Default</Radio.Button>
                <Radio.Button value="middle">Middle</Radio.Button>
                <Radio.Button value="small">Small</Radio.Button>
              </Radio.Group>
            </FormItem>
          </Form>
        </div>
        <Table {...this.state} columns={columns} dataSource={data} />
      </div>
    );
  }
}

ReactDOM.render(<Demo />, mountNode);
````

<style>
.components-table-demo-control-bar {
  margin-bottom: 10px;
}
.components-table-demo-control-bar .ant-form-item {
  margin-right: 16px;
  margin-bottom: 8px;
}
</style>
